<template>
  <div class="row m-0">
    <div class="col text-center">

      <img src="../assets/seat-logo.png" alt="logo" style="width: 141px;margin-top: 20px;margin-bottom: 50px;"/>

      <div class="my-menu">

        <div @click="selectedComponent = 'Models'" style="cursor: pointer;">
          <div class="my-button"
               :class="{'my-button-selected':selectedComponent === 'Models'}">Models
          </div>
          <button class="bottom-button"
                  :class="{'bottom-button-selected':selectedComponent === 'Models'}"></button>
        </div>

        <div @click="selectedComponent = 'Colors'" style="cursor: pointer;">
          <div class="my-button"
               :class="{'my-button-selected':selectedComponent === 'Colors'}">Colors
          </div>
          <button class="bottom-button"
                  :class="{'bottom-button-selected':selectedComponent === 'Colors'}"></button>
        </div>

        <div>
          <div @click="selectedComponent = 'Accessories'" style="cursor: pointer;">
            <div class="my-button"
                 :class="{'my-button-selected':selectedComponent === 'Accessories'}">Accessories
            </div>
            <button class="bottom-button"
                    :class="{'bottom-button-selected':selectedComponent === 'Accessories'}"></button>
          </div>
        </div>

        <div @click="selectedComponent = 'Summary'" style="cursor: pointer;">
          <div class="my-button"
               :class="{'my-button-selected':selectedComponent === 'Summary'}">Summary
          </div>
          <button class="bottom-button"
                  :class="{'bottom-button-selected':selectedComponent === 'Summary'}"></button>
        </div>

      </div>

      <!--<Transition :duration="{ enter: 500, leave: 800 }" mode="in-out" appear>-->
      <component :is="selectedComponent" :cars="cars" :selectedModel="selectedModel"></component>
      <!--</Transition>-->

      <div class="row m-0">
        <div class="col-md-3"></div>
        <div class="col-md-6 p-3">
          <div class="downslide"
               :style="{'marginTop':selectedComponent !== 'Colors'?'80px':'0'}">
            <img alt="selected car image" :src="require('../assets/cars/'+
        getSelectedCar.model+'/'+
        getSelectedCar.colors[getSelectedCar.selectedColor]+'.png')"
                 style="height: 100%;"/>
            <div class="vertical-line"></div>
            <div class="d-flex flex-column" style="width: 200px;padding: 10px;">
              <p class="downslide-text downslide-text-bold">Total</p>
              <p class="downslide-text">{{ getTotalPrice.toLocaleString('tr-TR') }} TL</p>
            </div>
            <button class="downslide-button" @click="slideTick()"><span class="downslide-button-text">{{
                getSlideText
              }}</span>
              <i class="bi bi-arrow-right" style="font-size: 15px;padding-bottom: 2px;"
                 v-if="selectedComponent !== 'Summary'"></i>
              <i class="bi bi-cart4" style="font-size: 15px;padding-bottom: 5px;" v-else></i>
            </button>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import Models from "@/components/Models"
import Colors from "@/components/Colors";
import Accessories from "@/components/Accessories";
import Summary from "@/components/Summary";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Main",
  components: {
    Models,
    Colors,
    Accessories,
    Summary
  },
  data() {
    return {
      publicPath: process.env.BASE_URL,
      selectedComponent: 'Models',
      selectedModel: 1,
      cars: [
        {
          id: 1,
          model: "ibiza",
          modelDescription: "Ibiza 1.3 Ecotech DSG",
          name: "IBIZA",
          price: 193500,
          description: "<b>193.500 TL</b>'den başlayan fiyatlarla",
          colors: ["red", "black", "blue", "gray", "white"],
          accessorries: [
            {
              id: 1,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 7500
            },
            {
              id: 2,
              description: "MAINTENANCE PROGRAM UPGRADE",
              price: 1250
            },
            {
              id: 3,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 13700
            },
            {
              id: 4,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 15475
            },
            {
              id: 5,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 9650
            },
            {
              id: 6,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 4000
            },
          ],
          selectedColor: 0,
          selectedAccessories: [1, 3],
        },
        {
          id: 2,
          model: "arona",
          modelDescription: "Arona 1.3 Ecotech DSG",
          name: "ARONA",
          price: 170000,
          description: "<b>170.000 TL</b>'den başlayan fiyatlarla",
          colors: ["red", "black", "blue", "gray", "white"],
          accessorries: [
            {
              id: 1,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 7500
            },
            {
              id: 2,
              description: "MAINTENANCE PROGRAM UPGRADE",
              price: 1250
            },
            {
              id: 3,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 13700
            },
            {
              id: 4,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 15475
            },
            {
              id: 5,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 9650
            },
            {
              id: 6,
              description: "SEAT FREE SYNC PACK EASY JET",
              price: 4000
            },
          ],
          selectedColor: 0,
          selectedAccessories: [2, 4],
        }
      ],
    }
  },
  methods: {
    slideTick() {
      switch (this.selectedComponent) {
        case 'Models':
          this.selectedComponent = 'Colors'
          break
        case 'Colors':
          this.selectedComponent = 'Accessories'
          break
        case 'Accessories':
          this.selectedComponent = 'Summary'
          break
      }
    }
  },
  computed: {
    getSelectedCar() {
      return this.cars.find(c => c.id === this.selectedModel)
    },
    getTotalPrice() {
      let car = this.getSelectedCar
      return car.price + car.selectedAccessories
          .map(accId => car.accessorries.find(acc => acc.id === accId).price)
          .reduce((f, l) => f + l)
    },
    getSlideText() {
      switch (this.selectedComponent) {
        case 'Models':
          return 'COLORS'
        case 'Colors':
          return 'ACCESSORIES'
        case 'Accessories':
          return 'SUMMARY'
        default:
          return 'BUY NOW'
      }
    }
  }
}
</script>

<style scoped>
.my-menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  max-width: 500px;
  margin: 0 auto;
  padding: 10px;
}

.my-button {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 17px;
  text-align: center;
  letter-spacing: 1px;
  color: #0F0F0F;
  cursor: pointer;
  mix-blend-mode: normal;
  opacity: 0.4;
}

.my-button-selected {
  opacity: 1;
}

.bottom-button {
  width: 14px;
  height: 4px;
  background-color: black;
  border: none;
  visibility: hidden;
}

.bottom-button-selected {
  visibility: visible;
}

.downslide {
  display: flex;
  flex-direction: row;
  width: 100%;
  max-width: 940px;
  min-width: 500px;
  height: 75px;
  background: #FFFFFF;
  box-shadow: 0 2px 70px rgba(0, 0, 0, 0.0703671);
  border-radius: 11px;
  margin: 0 auto 50px auto;
  text-align: left;
}

.downslide-button {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  background: #181818;
  border-radius: 0 11px 11px 0;
  height: 100%;
  width: 28%;
  color: white;
  margin-left: auto;
  border: none;
}

.downslide-button:hover {
  background: #363535;
}

.vertical-line {
  width: 1px;
  height: 55px;
  margin-top: 10px;
  border-right: 1px solid rgba(151, 151, 151, 0.2);
}

.downslide-text {
  font-style: normal;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: 1.7094px;
  color: #1C1C1C;
  margin: 0;
}

.downslide-text-bold {
  font-weight: 800;
  margin-bottom: 15px;
}

.downslide-button-text {
  font-family: 'Qanelas', serif;
  font-style: normal;
  font-weight: 700;
  font-size: 12px;
  letter-spacing: 2.78571px;
  color: #FFFFFF;
}

</style>