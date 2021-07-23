<template>
  <body>
  <div class="actions">
    <div class="autocomplete">
      <v-autocomplete
          auto-select-first
          solo-inverted
          label="Выберите валюту"
          :data="rates"
          :limit="10"
      ></v-autocomplete>
    </div>
    <div>
      <v-btn
          outlined
      >Add</v-btn>
    </div>
    </div>
  <div class="plates">
    <div class="block">Название<br>Значение 1<br>Дата последнего изменения</div>
    <div class="block">Название<br>Значение 2<br>Дата последнего изменения</div>
    <div class="block">Название<br>Значение 3<br>Дата последнего изменения</div>
  </div>
  <v-data-table :headers="headers">
  </v-data-table>
</body>
</template>

<script>
import axios from 'axios'
// import { cloneDeep } from "lodash"

export default {
  name: 'Rates',
  components: {

  },
  data: () => ({
    rates: [],
    errors: [],
    headers: [
      {text: 'Валюта', align: 'center', sortable: false, value: 'name'},
      {text: 'Значение', align: 'center', value: 'rate'},
      {text: 'Дата изменения', align: 'center', value: 'date'},
    ],
  }),
  methods: {

  },
  computed: {

  },
  created () {
    axios.get('https://www.cbr-xml-daily.ru/daily_json.js')
        .then(response => {
          this.rates = response.data.Valute
          console.log(this.rates)
        })
        .catch(e => {
          this.errors.push(e)
        })
  }
}
</script>

<style>
body {
  width:100%;
}
.autocomplete {
  width: 30%;
}
.actions {
  display: flex;
  justify-content: space-around;
}
.plates {
  display: flex;
  justify-content: space-around;
}
.block {
  width: 200px;
  height: 200px;
  border: 1px solid;
}
table {
  width: 100%;
}
thead, th {
  background-color: #fff;
  position: sticky;
  top: 0;
  z-index: 999;
}
</style>