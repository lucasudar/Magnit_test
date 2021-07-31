<template>
  <v-data-table :headers="headers"
                :items="array"
  >
  </v-data-table>
</template>

<script>
export default {
  name: "Table",
  props: {
    index: null,
    array: [],
  },
  watch: {
    index: function () {
      // console.log(this.array)
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