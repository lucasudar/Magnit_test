<template>
  <div class="plates">
    <p v-if="!plates.length">There are no data yet.</p>
    <v-card
        v-for="plate in plates"
        :key="plate"
        elevation="1"
    >
      <v-card-title>{{ plate.selectedRate }}</v-card-title>
      <v-card-subtitle>{{ plate.price }}</v-card-subtitle>
      <v-card-text>{{ plate.currentTimeStamp }}</v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "Cards",
  props: {
    card: Object
  },
  watch: {
    card: function () {
      this.plates.push(this.card)
    }
  },
  data: () => ({
    plates: [],
  }),
  methods: {

  },
  components: {
  },
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