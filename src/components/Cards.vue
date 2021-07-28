<template>
  <div class="plates">
    <p v-if="!plates.length">There are no data yet.</p>
    <v-card
        class="block"
        v-for="plate in plates"
        :key="plate"
        elevation="1"
    >
      <button type="button" class="close"
              @click="areYouSure"> x
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
    card: Object
  },
  watch: {
    card: function () {
      // let result
      // let checkArray = Object.values(this.card)
      // result = result.push(checkArray)
      // console.log(result)
      // if ()
      this.plates.push(this.card)
      // console.log(this.plates)
    },
    // plates: function () {
    //   console.log('plates array changed')
    //   let uniqIds = {}
    //   let filtered = this.plates.filter(obj => !uniqIds[obj.selectedRate] && (uniqIds[obj.selectedRate] = true));
    //   console.log(filtered)
    // },
  }
  ,
  data: () => ({
    plates: [],
  }),
  methods: {
    areYouSure: function () {
      if (confirm("Are you sure?")) {
        let plates = document.querySelectorAll('.block');
        for (let plate of plates) {
          plate.firstChild.onclick = () => plate.remove();
        }
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