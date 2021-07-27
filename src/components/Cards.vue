<template>
  <div class="plates">
    <p v-if="!plates.length">There are no data yet.</p>
    <ul>
      <li v-for="plate in plates"
          @card-submitted='addCard'
          :key="plate">
        <p>{{ plate.selectedRate }}</p>
        <p>Price: {{ plate.price }}</p>
        <p>Last modify: {{ plate.currentTimeStamp }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
// import Rates from './components/Rates.vue'

export default {
  name: "Cards",
  props: {
    card: {
      type: Object
    }
  },
  data: () => ({
    plates: [],
  }),
  methods: {
    addCard(card) {
      this.plates.push(card)
    }
  },
  components: {
    // Rates
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