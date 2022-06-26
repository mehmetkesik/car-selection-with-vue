<template>
  <div class="row">
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

      <br/><br/>

      <div class="downslide">
        <img alt="selected car image" :src="require('../assets/cars/'+
        getSelectedCar.model+'/'+
        getSelectedCar.colors[getSelectedCar.selectedColor]+'.png')"
             style="height: 100%;"/>
        <div class="vertical-line"></div>
        <div class="d-flex flex-column" style="width: 200px;">
          <p class="downslide-text downslide-text-bold" style="display: inline-block">fads</p>
          <p class="downslide-text" style="display: inline-block">fads</p>
        </div>
        <button class="downslide-button">Colors</button>
      </div>
      <br/><br/><br/><br/><br/>

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
          price: 193.500,
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
          price: 170.000,
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
  computed: {
    getSelectedCar() {
      return this.cars.find(c => c.id === this.selectedModel)
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
  width: 470px;
  height: 50px;
  background: #FFFFFF;
  box-shadow: 0 2px 70px rgba(0, 0, 0, 0.0703671);
  border-radius: 11px;
  margin: 0 auto;
  text-align: left;
}

.downslide-button {
  background: #181818;
  border-radius: 0 11px 11px 0;
  height: 100%;
  width: 120px;
  color: white;
  margin-left: auto;
  border: none;
}

.vertical-line {
  width: 1px;
  height: 30px;
  margin-top: 10px;
  border-right: 1px solid rgba(151, 151, 151, 0.2);
}

.downslide-text {
  font-style: normal;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: 1.7094px;
  color: #1C1C1C;
}

.downslide-text-bold {
  font-weight: 800;
}

</style>