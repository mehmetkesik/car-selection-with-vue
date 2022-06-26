<template>
  <div>
    <br/>
    <br/>
    <br/>
    <div class="row text-center">
      <div class="col-2"></div>

      <div class="col text-center" v-for="car in cars" :key="car.id">
        <div class="car-box text-center" @click="setViewedCar(car.id)"
             :style="{opacity:showedModel === car.id ? 1 : 0.3}">

          <p class="car-name">{{ car.name }}</p>
          <img :src="require('../assets/cars/'+car.model+'/'+car.colors[0]+'.png')" alt="car image"
               style="width: 500px;height: 250px;margin-top: 75px;"/>
          <div class="select-tick text-center" :style="{display: selectedModel === car.id ? 'flex':'none'}">
            <i class="bi bi-check-lg" style="color:lightgray;width: 100%;padding-top: 1px;font-size: 20px;"></i>
          </div>
          <div class="car-description">
            <p class="car-desc-text" v-html="car.description"
               :style="{display: showedModel === car.id ? 'inline':'none'}"></p>
            <button class="car-desc-button" @click="setSelectedModel(car.id)"
                    :style="{display: showedModel === car.id ? 'inline':'none'}">
              {{ selectedModel === car.id ? "Selected" : "Select" }}
            </button>
          </div>

        </div>
      </div>

      <div class="col-2"></div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Models",
  emits: ["keepSelection"],
  props: {
    cars: Array,
    selectedModel: Number,
  },
  data() {
    return {
      showedModel: this.cars[0]?.id
    }
  },
  methods: {
    setSelectedModel(id) {
      //this.$parent.$data.selectedModel = id
      //console.log(this.$parent.$data.selectedModel)
      this.$emit('keepSelection', 'Model', id)
    },
    setViewedCar(id) {
      this.showedModel = id
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
  width: 400px;
  height: 400px;
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

.select-tick {
  display: flex;
  justify-content: center;
  width: 33px;
  height: 33px;
  position: absolute;
  border-radius: 100%;
  background-color: #1C1C1C;
  margin-left: 250px;
  margin-top: 27px;
}

.car-description {
  display: flex;
  justify-content: center;
  position: absolute;
  margin-top: 300px;
  width: 200px;
  flex-direction: column;
}

.car-desc-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-size: 15px;
  line-height: 16px;
  text-align: center;
}

.car-desc-button {
  width: 100px;
  height: 30px;
  margin: 0 auto;
  background: #181818;
  border-radius: 15px;
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 700;
  font-size: 11px;
  line-height: 14px;
  text-align: center;
  letter-spacing: 2.5px;
  color: #FFFFFF;
  border: none;
}

.car-desc-button:hover {
  background: #464545;
}
</style>