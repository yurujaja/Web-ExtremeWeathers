<template>
  <div class="row q-pa-md">
    <div class="col">
      <GlobalEvents
        ref="mapViewer"
        class="flex flex-center"
        :current_phase="current_phase"
      />
      <!-- <div class="row q-pl-xl q-mt-xm justify-center"> -->
      <div class="col-12 col-md-10">
        <a>Legend</a> <br />
        <span id="positive-bar"></span>

        <br />
        <span id="negative-text">0</span>
        <!-- <span id="zero-text">0.0</span> -->
        <span id="positive-text">460</span>
      </div>
      <!-- </div> -->
    </div>

    <div class="col">
      <div style="margin-top: 15%; margin-left: 0%; margin-right: 15%">
        <strong class="text-primary" style="font-size: 300%">
          Extreme Weather Events: Global Explorer</strong
        >
        <div class="text-body1">
          <p>
            <br />
            Extreme weather events are becoming more and more frequent across
            the world. Globally, events that were previously considered
            1-in-50-year extreme heat events have become about
            <strong>five times</strong> more likely. <br />The globe shows the
            number of total extreme events in different time periods. Here the
            included types of extreme weathers are the above mentioned
            wildfires, storms, heatwaves and droughts, and floods.
          </p>
        </div>

        <div class="row item-center" style="justify-content: center">
          <div class=".col" style="padding: 2%">
            <q-btn
              :outline="btn1_activate"
              rounded
              size="lg"
              color="primary"
              label="1962 -- 1982"
              @click="updateData(1)"
            ></q-btn>
          </div>
          <div class=".col" style="padding: 2%">
            <q-btn
              :outline="btn2_activate"
              rounded
              size="lg"
              color="primary"
              label="1982 -- 2002"
              @click="updateData(2)"
            ></q-btn>
          </div>
          <div class=".col" style="padding: 2%">
            <q-btn
              :outline="btn3_activate"
              rounded
              size="lg"
              color="primary"
              label="2002 -- 2022"
              @click="updateData(3)"
            ></q-btn>
          </div>
        </div>
        <div>
          <strong class="text-primary" style="font-size: 220%">
            Number of Events</strong
          >
        </div>
        <q-space></q-space>
        <div>
          <strong class="text-primary" style="font-size: 250%">
            {{ current_phase }}</strong
          >
        </div>
      </div>
    </div>
  </div>
  <q-space class="q-ma-sm" />
  <q-space class="q-ma-sm" />
  <div>
    <LimitWidth
      ><div class="text-body1">
        <p>
          <br />
          Regarding the number of occurred extreme weather events, the most
          affected countries around the world are
          <strong>The United States of America</strong>,
          <strong>China</strong> and <strong>India</strong> .
        </p>
      </div></LimitWidth
    >
  </div>

  <!-- <div class="row">
    <div class="col center" style="margin-left: 10%">
      >
      <CountryEventsChart />
    </div>
  </div> -->

  <div class="row">
    <div class="col-8"><CountryEventsChart /></div>
    <div class="col-4"><TypesPieChart /></div>
  </div>
</template>

<script>
import { ref } from "vue";
import GlobalEvents from "../maps/GlobalEvents.vue";
import CountryEventsChart from "../charts/CountriesEvents.vue";
import TypesPieChart from "../charts/TypesDistribution.vue";
import LimitWidth from "../utils/LimitWidth.vue";

export default {
  name: "GlobalSituation",
  components: {
    GlobalEvents,
    CountryEventsChart,
    LimitWidth,
    TypesPieChart,
  },
  data() {
    return {
      num_events: " ",
      current_phase: "Phase1Events",
      btn1_activate: false,
      btn2_activate: true,
      btn3_activate: true,
    };
  },
  setup() {
    return {
      slide: ref("first"),
      autoplay: ref(true),
    };
  },
  methods: {
    updateData(index) {
      if (index == 1) {
        this.current_phase = "Phase1Events";
        this.btn1_activate = false;
        this.btn2_activate = true;
        this.btn3_activate = true;
      } else if (index == 2) {
        this.current_phase = "Phase2Events";
        this.btn1_activate = true;
        this.btn2_activate = false;
        this.btn3_activate = true;
      } else if (index == 3) {
        this.current_phase = "Phase3Events";
        this.btn1_activate = true;
        this.btn2_activate = true;
        this.btn3_activate = false;
      }
    },
  },
};
</script>

<style scoped>
#positive-bar {
  display: inline-block;
  width: 50%;
  height: 15px;
  margin-right: 0;
  margin-left: 10px;
  background: linear-gradient(
    to right,
    rgb(255, 255, 208),
    rgb(254, 162, 70),
    rgb(246, 72, 41),
    rgb(128, 0, 38)
  );
}

#positive-text {
  display: inline-block;
  width: 10%;
  height: 15px;
  margin-right: 0px;
  margin-left: 0;
  text-align: left;
}

#negative-text {
  display: inline-block;
  width: 50%;
  height: 15px;
  margin-right: 0px;
  margin-left: 10%;
  text-align: left;
}
</style>
