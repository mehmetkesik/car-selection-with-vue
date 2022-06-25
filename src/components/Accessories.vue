<template>
  <br/>
  <br/>
  <br/>
  <p class="car-acc-text">Seçtiğin araca ait özellikler, konforun ve yaşam stilini belirler.</p>
  <div class="row text-center" style="max-width: 950px;margin: 0 auto">
    <div class="col-md-4 text-center" v-for="acc in car.accessorries" :key="acc.id">
      <div class="accessories" :class="{'accessories-select':isSelectedAcc(acc)}">
        <p :class="{'accessories-select-text':isSelectedAcc(acc),
        'accessories-text':!isSelectedAcc(acc)}">{{ acc.description }}</p>
        <p :class="{'accessories-select-text':isSelectedAcc(acc),
        'accessories-text':!isSelectedAcc(acc)}" style="margin-top: 50px">{{ acc.price.toLocaleString('tr-TR') }} TL</p>
        <button class="acc-select-button" @click="setAccessories(acc.id)" v-if="isSelectedAcc(acc)">
          <i class="bi bi-check-lg acc-select-tick-select"></i>
        </button>
        <button class="acc-select-button" @click="setAccessories(acc.id)" v-if="!isSelectedAcc(acc)"
                style="border: 1px solid lightgray;">
          <i class="bi bi-check-lg acc-select-tick" style="visibility: hidden"></i>
        </button>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Accessories",
  props: {
    cars: Array,
    selectedModel: Number
  },
  data() {
    return {
      car: this.cars.find(car => car.id === this.selectedModel)
    }
  },
  methods: {
    setAccessories(i) {
      let selectedModel = this.$parent.$data.cars.find(car => car.id === this.selectedModel)
      let accIndex = selectedModel.selectedAccessories.find(id => id === i)
      if (accIndex) {
        selectedModel.selectedAccessories = selectedModel.selectedAccessories.filter(id => id !== i)
      } else {
        selectedModel.selectedAccessories.push(i)
      }
    },
    isSelectedAcc(acc) {
      return !!this.$parent.$data.cars.find(car => car.id === this.selectedModel)
          .selectedAccessories.find(id => id === acc.id)
    }
  }
}
</script>

<style scoped>
.accessories {
  width: 250px;
  height: 235px;
  border-radius: 11px;
  margin: 0 auto 30px auto;
  border: 1px solid rgba(151, 151, 151, 0.3);
  padding: 50px 20px 20px 20px;
}

.accessories-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #0F0F0F;
}

.accessories-select {
  background: #292929;
  border: 1px solid #6A6A6A;
  opacity: 1;
}

.accessories-select-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  letter-spacing: 1px;
  color: #FFFFFF;
}

.acc-select-button {
  background: none;
  border-radius: 100%;
  border: none;
  padding: 0;
  margin-top: 13px;
}

.acc-select-tick-select {
  color: lightgray;
  font-size: 22px;
  background: #6A6A6A;
  mix-blend-mode: normal;
  opacity: 0.3;
  border-radius: 100%;
  padding: 0 4px;
  border: 2px solid white;
}

.acc-select-tick {
  color: lightgray;
  font-size: 22px;
  background: #6A6A6A;
  mix-blend-mode: normal;
  opacity: 0.3;
  border-radius: 100%;
  padding: 0 4px;
  border: 2px solid white;
}

.car-acc-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 18px;
  text-align: center;
  color: #1C1C1C;
  width: 300px;
  margin: 0 auto 50px auto;
}

</style>