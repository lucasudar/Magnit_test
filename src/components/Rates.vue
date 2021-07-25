<template>
  <body>
  <div class="actions" @submit.prevent="onSubmit">
    <div class="autocomplete">
      <v-autocomplete
          label="Введите валюту"
          item-text="Name"
          solo
      ></v-autocomplete>
      <select v-model="selectedRate">
        <option v-for="rate in rates"
                :value="rate.Name"
                :key="rate.Name"
                >
          {{ rate.Name }}
        </option>
      </select>
    </div>
    <div>
      <v-btn
          @click="submit"
          outlined
      >Add</v-btn>
    </div>
    </div>
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
    selectedRate: null,
    price: null,
    date: null,

  }),
  methods: {
    submit() {
      console.log(this.selectedRate)
    },

  },
  computed: {

  },
  created () {
    axios.get('https://www.cbr-xml-daily.ru/daily_json.js')
        .then(response => {
          this.rates = response.data.Valute
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
  width: auto;
  border-style: groove;
}
.actions {
  display: flex;
  justify-content: space-around;
}

</style>