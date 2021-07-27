<template>
  <div class="plates">
<!--  <button @click="addPlate(card)">addPlate</button>-->
    <p v-if="!plates.length">There are no data yet.</p>
    <ul>
      <li v-for="plate in plates"
          :key="plate">
        <p>{{ plate.selectedRate }}</p>
        <p>Price: {{ plate.price }}</p>
        <p>Last modify: {{ plate.currentTimeStamp }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Cards",
  props: {
    card: Object
  },
  data: () => ({
    plates: [],
  }),
  methods: {
    // addPlate(card) {
    //   this.plates.push(card)
    // }
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