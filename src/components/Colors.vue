<template>
  <div>
    <br/>
    <br/>
    <br/>
    <div class="row text-center">
      <div class="col text-center">
        <div class="car-color">
          <p class="car-color-text">Hayalindeki araca dair rengini seç, tarzını hemen yansıt</p>
          <p class="car-name">{{ car.name }}</p>
          <img class="car-image" :src="require('../assets/cars/'+car.model+'/'+car.colors[car.selectedColor]+'.png')"
               alt="car image"/>
        </div>

      </div>
    </div>
    <div class="row text-center">
      <div class="col text-center">
        <button class="colors-select m-2" @click="setSelectedColor(index)" v-for="(color, index) in car.colors"
                :key="color"
                :style="{backgroundImage: 'url('+require('../assets/cars/'+car.model+'/colors/'+color+'.jpg')+')'}"
                :class="{'colors-select-selected':car.selectedColor === index}">
          <i class="bi bi-check-lg colors-select-tick"
             :style="{visibility:/*this.$parent.$data.cars.find(car => car.id === this.selectedModel)*/car.selectedColor === index ?
        'visible':'hidden'}"></i>
        </button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Colors",
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
    setSelectedColor(index) {
      //this.$parent.$data.cars.find(car => car.id === this.selectedModel).selectedColor = index
      this.$emit('keepSelection', 'Color', index)
    }
  }
}
</script>

<style scoped>
.car-color {
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin: 0 auto;
}

.car-color-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 18px;
  text-align: center;
  color: #1C1C1C;
  width: 200px;
  margin: 0 auto 30px auto;
}

.car-name {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 800;
  font-size: 200px;
  line-height: 174px;
  text-align: center;
  letter-spacing: -6.48px;
  color: #000000;
  mix-blend-mode: normal;
  opacity: 0.09;
  z-index: -1;
}

.car-image {
  width: 500px;
  height: 250px;
  position: relative;
  margin: 0 auto;
  bottom: 140px;
}

.colors-select {
  position: relative;
  bottom: 120px;
  width: 50px;
  height: 50px;
  background-size: cover;
  border-radius: 100%;
  border: none;
  text-align: left;
  background-clip: content-box;
  padding: 4px;
}

.colors-select-selected {
  border: 1px solid lightgray;
}

.colors-select-tick {
  color: lightgray;
  font-size: 16px;
  background-color: black;
  border-radius: 100%;
  padding: 0 2px;
  border: 2px solid white;
  position: relative;
  top: -15px;
  left: -10px;
}
</style>