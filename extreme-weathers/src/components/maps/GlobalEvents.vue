<template>
  <!--  3D Globe Map -->
  <div id="globeViz"></div>
</template>

<script>
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

    autoRotate(auto = true) {
      // Add auto-rotation
      this.world.controls().autoRotate = auto;
      if (auto) {
        this.world.controls().autoRotateSpeed = this.rotationSpeed;
      }
    },

    showLayer() {
      // Show layer
      const colorScale = d3.scaleSequentialSymlog(d3.interpolateYlOrRd);
      const current_phase = this.current_phase;
      const getVal = (feat) => feat.properties[current_phase];
      var sumVal;
      //colorScale.domain([0, maxVal]);
      fetch(this.dataFilePath)
        .then((res) => res.json())
        .then((countries) => {
          sumVal = countries.features
            .map(getVal)
            .reduce((partialSum, a) => partialSum + a, 0);
          this.$emit("numEvents", sumVal);
          const maxVal = 450;
          colorScale.domain([0, maxVal]);
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

    this.$watch("current_phase", () => {
      this.initMap();
    });
  },
};
</script>

<style scoped></style>
