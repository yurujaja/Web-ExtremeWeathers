<template>
  <div class="row items-center" style="margin: 2%">
    <div class=".col-8"><HeatEuropeMap /></div>
    <div class=".col-4"><TemperatureGauge /></div>
  </div>
  <q-img src="images/Wildfires_in_southwest_France.gif" width="40%"></q-img>
  <div>
    <LossEuropeMap />
  </div>
</template>

<script>
import { ref } from "vue";
import HeatEuropeMap from "../maps/HeatEurope.vue";
import TemperatureGauge from "../charts/TemperatureGauge.vue";
import LossEuropeMap from "../maps/LossesEurope.vue";
export default {
  name: "EuropeanSituation",
  components: {
    HeatEuropeMap,
    TemperatureGauge,
    LossEuropeMap,
  },
  setup() {},
};
</script>

<!-- <style lang="sass" scoped>
  strong
    color: #ff6600
    font-size: 105%


  .text-body1
    text-align: left
    font-size: 130%


  .custom-caption
    text-align: center
    padding: 12px
    color: white
    background-color: rgba(0, 0, 0, .3)
  </style> -->
<style scoped></style>
