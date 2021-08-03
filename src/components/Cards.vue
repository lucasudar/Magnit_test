<template>
  <div class="plates">
    <p v-if="!plates.length">There are no data yet.</p>
    <v-card
        class="block"
        v-for="(plate, index) in plates"
        :key="plate"
        @click="showData(index)"
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
import axios from "axios";

export default {
  name: "Cards",
  props: {
    card: Object,
    updatedPriceArray: [],
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
        }
      }
      this.$emit('send-plates', this.plates)
    },
    plates: function () {
      console.log('изменение в плейтс')
      // TODO: для всех карточек в массиве this.plates получать новый price каждую минуту через api и заменять в массиве.
      // TODO: Записывать получаемые значения в объект, а далее массив этих объектов передавать по клику в items компонента table.vue

      axios.get('https://www.cbr-xml-daily.ru/daily_json.js')
          .then(response => {
            this.updatedPriceArray = response.data.Valute
            let updatedRates = Object.values(this.updatedPriceArray)
            console.log(updatedRates)
            console.log(this.plates)
            // TODO: пробежаться по именам в массиве plates,
            // TODO: найти новые значения курса во вновь полученном массиве updatedRates и перезаписать в plates
            // for (let obj in updatedRates) {
            //   if (updatedRates[obj].Name == this.plates.%INDEX%.selectedRate) {
            //     this.plates.%INDEX%.Value = updatedRates[obj].Value
            //   }
            //   }
          })
          .catch(error => {
            console.log(error);
          })
    }
  },
  data: () => ({
    plates: [],
  }),
  methods: {
    areYouSure: function (index) {
      if (confirm("Are you sure?")) {
        this.plates.splice(index, 1)
      }
    },
    showData: function (index) {
      this.$emit('show-data', index)
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