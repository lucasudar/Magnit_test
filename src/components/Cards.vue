<template>
  <div class="plates">
    <p v-if="!plates.length">There are no data yet.</p>
    <v-card
        class="block"
        v-for="(plate, index) in plates"
        :key="plate"
        elevation="1"
    >
      <button type="button" class="close"
              @click="areYouSure(index)"> x
      </button>
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
    card: Object,
  },
  watch: {
    card: function () {
      if (this.plates.length < 1) {
        this.plates.push(this.card)
      } else {
        let allRates = [];
        this.plates.forEach(obj => allRates.push(Object.values(obj).slice(0, 1).join()))
        if (allRates.includes(this.card.selectedRate)) {
          alert('Can\'t add, this is a copy!')
        } else {
          this.plates.push(this.card)
          console.log(this.plates[1])
        }
      }
    },
  },
  data: () => ({
    plates: [],
  }),
  methods: {
    areYouSure: function (index) {
      if (confirm("Are you sure?")) {
        this.plates.splice(index, 1)
      } else return;
    }
  },
  components: {},
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

.close {
  position: absolute;
  right: 1px;
  margin-bottom: 15px;
  width: 32px;
  height: 32px;
  border: none;
  font-size: 20px;
  cursor: pointer;
  background: transparent;
}
</style>