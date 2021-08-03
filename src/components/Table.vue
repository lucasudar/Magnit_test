<template>
  <v-data-table :headers="headers"
                :items="array"> <!-- TODO: передавать в items массив объектов одной валюты с разными датами изменений -->
  </v-data-table>
</template>

<script>
export default {
  name: "Table",
  props: {
    index: Number,
    array: [],
  },
  watch: {
    index: function () {
      console.log(this.index) // index нажатого элемента на блоке
      console.log(this.array) // array массив плашек
    }
  },
  data: () => ({
    headers: [
      {text: 'Валюта', align: 'center', sortable: false, value: 'selectedRate'},
      {text: 'Значение', align: 'center', value: 'price'},
      {text: 'Дата изменения', align: 'center', value: 'currentTimeStamp'},
    ],
  }),
  methods: {}
}
</script>

<style scoped>
table {
  width: 100%;
}
</style>