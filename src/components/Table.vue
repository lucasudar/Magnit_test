<template>
  <v-data-table :headers="headers">
  </v-data-table>
</template>

<script>
export default {
  name: "Table",
  data: () => ({
    headers: [
      {text: 'Валюта', align: 'center', sortable: false, value: 'name'},
      {text: 'Значение', align: 'center', value: 'rate'},
      {text: 'Дата изменения', align: 'center', value: 'date'},
    ],
  })
}
</script>

<style scoped>
table {
  width: 100%;
}
</style>