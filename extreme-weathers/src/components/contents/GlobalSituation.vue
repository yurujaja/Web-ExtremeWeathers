<template>
  <div class="row q-pa-md" style="margin-top: 3%">
    <div class="col" style="margin: 0 auto">
      <GlobalEvents
        ref="mapViewer"
        class="flex flex-center"
        :current_phase="current_phase"
        @numEvents="getNum"
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
      <div style="margin: 0 auto">
        <strong class="text-primary" style="font-size: 300%">
          Extreme Weather Events: <br />Global Explorer</strong
        >
        <div class="text-body1">
          <p>
            <br />
            Extreme weather events are becoming more and more frequent across
            the world. Globally, events that were previously considered
            1-in-50-year extreme heat events have become about
            <strong>five times</strong> more likely.
            <q-space></q-space>
            <br />The globe shows the number of total extreme events in
            different time periods. Here the included types of extreme weathers
            are the above mentioned wildfires, storms, heatwaves and droughts,
            and floods.
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
          <br />
          <strong class="text-primary" style="font-size: 200%">
            Number of Events</strong
          >
        </div>
        <q-space></q-space>
        <div>
          <strong class="text-primary" style="font-size: 220%">
            {{ num_events }}</strong
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
          Over the last 20 years, the world has witnessed the frequency of
          occurred extreme events increasing dramatically. Among the above
          mentioned types of extreme weather events, storms and floods account
          for a large proportion. Regarding the number of occurred extreme
          weather events, the most affected countries around the world are
          <strong>The United States of America</strong>,
          <strong>China</strong> and <strong>India</strong> .
          <br />
          The charts below illustrate the distribution of the types of different
          extremes that occurred from 2002-2022 in these countries.
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

  <div>
    <h4><p>Extreme Weathers and Climate Change</p></h4>
    <div class="row" style="margin-left: 10%">
      <div class="col">
        <div style="margin-top: 2%; margin-left: 0%; margin-right: 5%">
          <strong class="text-primary" style="font-size: 170%">
            How climate change affects extreme weather around the world</strong
          >
          <div class="text-body1">
            <p>
              <br />
              Many weather and climate extremes happen naturally, even without
              climate change. But Earth’s changing climate does change where and
              how often some extreme events take place, and how strong those
              events are. Scientists have published more than 400 peer-reviewed
              studies looking at weather extremes around the world, from
              <a
                herf="https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2021GL095496"
                >wildfires in the US</a
              >
              and
              <a
                herf="https://www.worldweatherattribution.org/climate-change-made-devastating-early-heat-in-india-and-pakistan-30-times-more-likely/"
                >heatwaves in India and Pakistan</a
              >
              to
              <a
                herf="https://rmets.onlinelibrary.wiley.com/doi/abs/10.1002/joc.6030"
                >typhoons in Asia</a
              >
              and record-breaking
              <a
                href="https://rmets.onlinelibrary.wiley.com/doi/10.1002/asl.1033"
                >rainfall in the UK</a
              >. The result is mounting evidence that human activity is raising
              the risk of some types of extreme weather, especially those linked
              to heat.<q-space></q-space>
              <ul>
                <li>71% of the 504 extreme weather events and trends included in
              the map were found to be made more likely or more severe by
              human-caused climate change. </li><q-space></q-space>
              <li>9% of events
              or trends were made less likely or less severe by climate change,
              meaning 80% of all events experienced some human impact. The
              remaining 20% of events and trends showed no discernible human
              influence or were inconclusive. </li><q-space></q-space>
              <li>Of the 152 extreme heat events that have been assessed by
              scientists, 93% found that climate change made the event or trend
              more likely or more severe. </li><q-space></q-space>
              <li>For the 126 rainfall or flooding
              events studied, 56% found human activity had made the event more
              likely or more severe. For the 81 drought events studied, it’s
              68%. </li>
              </ul>

            </p>
          </div>
        </div>
      </div>
      <div class="col">
        <q-img src="images/climate_change.jpg" ></q-img>
      </div>
    </div>
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
    LimitWidth,
    CountryEventsChart,
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
    getNum(data) {
      this.num_events = data;
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
