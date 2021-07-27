<template>
  <body>
  <div class="actions">
<!--    <div class="autocomplete">-->
<!--      <v-autocomplete-->
<!--          label="Введите валюту"-->
<!--          item-text="Name"-->
<!--          solo-->
<!--      ></v-autocomplete>-->
<!--    </div>-->
    <form style="border-style: groove">
      <select v-model="selectedRate">
        <option v-for="rate in rates"
                :value="rate.Name"
                :key="rate.Name"
        >
          {{ rate.Name }}
        </option>
      </select>
    </form>
<!--    <span><p>{{ card }}</p></span>-->
    <div>
      <v-btn
          @click="onSubmit(card)"
          outlined
      >Add
      </v-btn>
    </div>
  </div>
  </body>
</template>

<script>
import axios from 'axios'
import { cloneDeep } from "lodash"

export default {
  name: 'Rates',
  components: {
      // Cards: () => import('./components/Cards'),
  },
  props: {
    card: {
      type: Object
    }
  },
  data: () => ({
    rates: [],
    errors: [],
    price: null,
    selectedRate: null,
    currentTimeStamp() {
      let date = new Date()

      let dd = date.getDate()
      if (dd < 10) dd = '0' + dd

      let mm = date.getMonth() + 1
      if (mm < 10) mm = '0' + mm

      let yy = date.getFullYear()
      if (yy < 10) yy = '0' + yy

      let hh = date.getHours()
      if (hh < 10) hh = '0' + hh

      let min = date.getMinutes()
      if (min < 10) min = '0' + min

      return dd + '.' + mm + '.' + yy + ' ' + hh + ':' + min
    },
  }),
  methods: {
    onSubmit () {
      let card = {
        selectedRate: this.selectedRate,
        price: "price",
        currentTimeStamp: this.currentTimeStamp(),
      }
      console.log(card)
      this.$emit('card-submitted', this.card)
      this.selectedRate = null
      console.log('message emit from child component')
    },
  },
  computed: {
    getValue: function () {
      return this.rates.filter(function (element) {
        let elementCopy = cloneDeep(element)
        if (elementCopy.Name === this.selectedRate) {
          return elementCopy.Value
        }
      })
    }
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
.actions {
  display: flex;
  justify-content: space-around;
}
</style>