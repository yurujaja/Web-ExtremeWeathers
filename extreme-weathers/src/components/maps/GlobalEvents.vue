<template>
  <!--  3D Globe Map -->
  <div id="globeViz" style="margin: -10%; margin-bottom: -16%"></div>
</template>

<script>
//import { stringLiteral } from "@babel/types";
import * as d3 from "d3";
import Globe from "globe.gl";

export default {
  name: "GlobalEvents",
  props: {
    current_phase: String,
  },
  data: function () {
    return {
      world: null,
      rotationSpeed: 0.9,
      globeColorScale: d3.scaleSequentialSqrt(d3.interpolateYlOrRd),
      dataFilePath: "data/global_events.geojson",
    };
  },
  methods: {
    initMap() {
      // Initialize the globe
      this.world = Globe()(document.getElementById("globeViz"))
        .backgroundColor("rgba(0,0,0,0)")
        .showGlobe(false)
        .showAtmosphere(false);
      this.showLayer();
      this.autoRotate(true);
    },

    numberWithCommas(x) {
      // Format numbers: 1,000,000,000
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },

    // resizeMap(height, width) {
    //   // Resize the globe
    //   this.world.width([width]);
    //   this.world.height([height]);
    // },

    autoRotate(auto = true) {
      // Add auto-rotation
      this.world.controls().autoRotate = auto;
      if (auto) {
        this.world.controls().autoRotateSpeed = this.rotationSpeed;
      }
    },

    showLayer() {
      // Show layer
      //const getVal = (feat) => feat.properties[this.dataColumn];
      const transferVal = (feat) => Math.log(Math.abs(feat));
      console.log(this.phase);
      const colorScale = d3.scaleSequentialSqrt(d3.interpolateYlOrRd);
      const current_phase = "Phase3Events";
      const getVal = (feat) => feat.properties[current_phase];
      //colorScale.domain([0, maxVal]);
      fetch(this.dataFilePath)
        .then((res) => res.json())
        .then((countries) => {
          // const minVal = Math.min(...countries.features.map(getVal));
          // const maxVal = Math.max(...countries.features.map(getVal));
          //const maxVal = Math.max(...countries.features.map(getVal));
          const maxVal = 250;
          colorScale.domain([0, maxVal]);

          // this.positiveColorScale.domain([0, transferVal(maxVal)]);
          // this.negativeColorScale.domain([0, transferVal(-minVal)]);
          this.world
            .polygonsData(
              countries.features.filter(
                (d) => d.properties.original_ISO_A2 !== "AQ"
              )
            )
            .polygonAltitude(0.06)
            .polygonCapColor((feat) => colorScale(getVal(feat)))
            .polygonSideColor(() => "rgba(250, 150, 0, 0.10)")
            .polygonStrokeColor(() => "#111")
            .polygonLabel(
              ({ properties: d }) => `
          <b>${d.ADMIN} (${d.original_ISO_A2}):</b> <br />
         Number of Events: <i>${d[current_phase]}</i><br/>

        `
            )
            .onPolygonHover((hoverD) =>
              this.world
                .polygonAltitude((d) => (d === hoverD ? 0.12 : 0.06))
                .polygonCapColor((d) =>
                  d === hoverD ? "steelblue" : colorScale(getVal(d))
                )
            )
            .polygonsTransitionDuration(300);
        });
    },
  },
  mounted() {
    this.initMap();
  },
};
</script>

<style scoped></style>
