<template>
  <div>
    <LimitWidth
      ><div class="text-body1">
        <br />
        <p>
          "Europe presents a live picture of a warming world and reminds us that
          even well prepared societies are not safe from impacts of extreme
          weather events", WMO secretary-general Petteri Taalas said
          <a
            href="https://library.wmo.int/index.php?lvl=notice_display&id=22152#.Y773dHbMLGK"
            >in a statement</a
          >.
        </p>
        <q-space></q-space>
        <p>
          From 1991 to 2021, temperatures over Europe warmed at an average of
          0.5 degrees Celsius per decade, while the global average was just 0.2
          degrees Celsius, according to the
          <a
            href="https://library.wmo.int/index.php?lvl=notice_display&id=22152#.Y773dHbMLGK"
            >report</a
          >. It found that Alpine glaciers lost 30 metres in ice thickness
          between 1997 and 2021, while the Greenland ice sheet is melting
          quickly and contributing to accelerating sea level rise. Some
          scientists are calling Europe a "heatwave hotspot" as the number of
          extreme temperature events on the continent increases faster than in
          other regions due to changes in atmospheric circulation.
        </p>
        <q-space></q-space>
        <p>
          The map below shows the countries that experience temperatures
          creeping over 40 degreees Celsius in Europe from 1980 to 2022, and
          much of western Europe are affected most. The temperature gauge
          indicate the average temperatures of July in Paris since the 21st
          century.
        </p>
      </div></LimitWidth
    >
  </div>

  <div class="row items-center" style="margin-left: 2%">
    <div class="col"><HeatEuropeMap /></div>
    <div class="col">
      <TemperatureGauge />
    </div>
  </div>
  <q-space class="q-ma-sm" />
  <q-space class="q-ma-sm" />

  <div class="row items-center q-pa-md" style="margin-left: 5%">
    <div class="col-4">
      <q-img
        src="images/Wildfires_in_southwest_France.gif"
        width="110%"
      ></q-img>
    </div>

    <div class="col-6">
      <div class="text-body1" style="margin-left: 15%; width: 110%">
        <p style="text-align: center; font-size: 120%">
          <strong>Why is Europe so impacted?</strong>
        </p>
        <br />
        <p>
          The reason Europe is warming faster than elsewhere has to do with the
          fact that a large part of the continent is in the
          <strong>sub-Arctic and Arctic</strong>.The WMO divides the world into
          six regions, with "Europe" comprising 50 countries and half of the
          Arctic, the fastest warming place on Earth.
        </p>
        <q-space></q-space>
        <p>
          Scientists also say Europe is impacted by
          <strong>climate feedbacks</strong>, which exacerbate existing
          phenomena. For example, fewer clouds over Europe during the summer has
          meant more sun and heat hits the earth, heating it even more.
          Additionally, Europe is particularly vulnerable to heat, with its
          <strong>dense urbanisation</strong> and ageing population.
        </p>
        <q-space></q-space>
        <p>
          The left visual shows fires and burn scars near the town of Cazaux in
          the southern Gironde region in France.The animation comprises images
          acquired on 12 July before the fires broke out and images acquired on
          17 July when the fires were active. The difference is clear to see.
        </p>
      </div>
    </div>
  </div>

  <LimitWidth
    ><div class="text-body1">
      <br />
      <p style="text-align: center; font-size: 120%">
        <strong
          >Economic losses and fatalities from weather- and climate-related
          events in Europe</strong
        >
      </p>
      <p>
        All regions of Europe face economic losses and fatalities from weather
        and climate extremes every year. To support policy processes on climate
        change adaptation, data on these losses must be collected and reported
        across EEA member countries and in a coherent way over decades.
      </p>
      <q-space></q-space>
      <p>
        Between 1980 and 2020, total economic losses from weather- and
        climate-related events amounted to EUR
        <strong>450-520 billion</strong> (in 2020 euros) in the 32 EEA member
        countries (EEA-32). Between only one quarter and one third of these
        losses were insured. Based on data from two separate sources (<a
          href="http://www.risklayer.com/de/service/catdat/"
          >CATDAT</a
        >
        and
        <a
          href="https://www.munichre.com/en/solutions/for-industry-clients/natcatservice.html"
          >NatCatSERVICE</a
        >
        ), fatalities during the same period amounted to between
        <strong> 85,000 and 145,000</strong>.
      </p>
      <q-space></q-space>
      <p></p></div
  ></LimitWidth>
  <div style="margin-left: 10%">
    <LossEuropeMap />
  </div>
</template>

<script>
import { ref } from "vue";
import HeatEuropeMap from "../maps/HeatEurope.vue";
import TemperatureGauge from "../charts/TemperatureGauge.vue";
import LossEuropeMap from "../maps/LossesEurope.vue";
import LimitWidth from "../utils/LimitWidth.vue";

export default {
  name: "EuropeanSituation",
  components: {
    HeatEuropeMap,
    TemperatureGauge,
    LossEuropeMap,
    LimitWidth,
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
