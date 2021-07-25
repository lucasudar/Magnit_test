<template>
  <div class="plates">
    <div class="block">Название<br>Значение<br>Дата последнего изменения</div>
    <div class="block">Название<br>Значение<br>Дата последнего изменения</div>
    <div class="block">Название<br>Значение<br>Дата последнего изменения</div>
  </div>
</template>

<script>
export default {
  name: "Cards"
}
</script>

<style scoped>
.plates {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}
.block {
  width: 200px;
  height: 200px;
  border: 1px solid;
}
</style>