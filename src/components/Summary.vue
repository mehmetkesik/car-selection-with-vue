<template>
  <br/>
  <br/>
  <br/>
  <div class="row p-5">
    <div class="col-md-6">
      <div class="car-box text-center" style="margin-right: 0">
        <p class="car-name">{{ car.name }}</p>
        <img :src="require('../assets/cars/'+car.model+'/'+car.colors[car.selectedColor]+'.png')" alt="car image"
             style="width: 500px;height: 250px;margin-top: 75px;"/>
      </div>
    </div>
    <div class="col-md-6">
      <div class="summary-description">
        <h3 class="summary-head">Model</h3>
        <p class="summary-text">{{ car.modelDescription }}</p>
        <hr class="opacity-25"/>
        <h3 class="summary-head">Color</h3>
        <p class="summary-text">
          {{ prettyColor(car.colors[$parent.$data.cars.find(car => car.id === this.selectedModel).selectedColor]) }}</p>
        <hr class="opacity-25"/>
        <h3 class="summary-head">Accessories</h3>
        <p class="summary-text">
          <span v-for="(acc, index) in car.selectedAccessories.map(x => car.accessorries.find(a => a.id === x))"
                :key="acc.id">{{ prettyAcc(acc.description) }} <span
              v-if="index !== car.selectedAccessories.length-1"> + </span> </span>
        </p>
      </div>

    </div>
  </div>

</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Summary",
  emits: ["keepSelection"],
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
    prettyAcc(str) {
      return str.split(' ').map(letter => letter.charAt(0).toUpperCase() + letter.slice(1).toLowerCase()).join(' ')
    },
    prettyColor(str) {
      return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase()
    }
  }
}
</script>

<style scoped>
.car-box {
  display: flex;
  justify-content: center;
  mix-blend-mode: normal;
  border: 1px solid rgba(0, 0, 0, .06);;
  border-radius: 100%;
  max-width: 400px;
  max-height: 400px;
  margin: 0 auto;
}

.car-name {
  position: absolute;
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 800;
  font-size: 100px;
  line-height: 174px;
  text-align: center;
  letter-spacing: -6.48px;
  color: #000000;
  mix-blend-mode: normal;
  opacity: 0.09;
  margin-top: 10px;
  z-index: -1;
}

.summary-description {
  margin-left: 0;
  text-align: left;
  width: 250px;
}

.summary-head {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 700;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #0F0F0F;
  margin-bottom: 20px;
}

.summary-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 19px;
  color: #1C1C1C;
  mix-blend-mode: normal;
  opacity: 0.38;
  margin-bottom: 40px;
}

hr {
  background-color: lightgray;
}
</style>