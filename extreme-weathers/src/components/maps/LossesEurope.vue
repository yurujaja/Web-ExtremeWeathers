<template>
  <div class="container justify-center items-center content-center">
    <div id="globalMap"></div>

    <div class="map-overlay" id="legend">
      <div class="q-gutter-sm">
        <q-radio
          v-model="loss_type"
          val="lossEuro"
          label="Losses (million EUR)"
          color="teal"
          v-on:click.enter="updateData"
        ></q-radio>
        <q-radio
          v-model="loss_type"
          val="fatalities"
          label="Fatalities"
          color="light-green-14"
          v-on:click.enter="updateData"
        ></q-radio>
      </div>
      <div style="text-align: left" v-for="item in legend_items" :key="item">
        <span
          class="legend-key"
          v-bind:style="'background-color:' + item.color"
        ></span
        ><span>{{ item.value }}</span>
      </div>

      <q-space class="q-ma-sm" />
      <label id="year">Year: {{ sliderValue }}</label>
    </div>
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";

export default {
  name: "LossEuropeMap",
  data() {
    return {
      data_dir: "data/europe_losses_1980_2020.geojson",
      loss_type: "lossEuro",

      map: "",
      accessToken:
        "pk.eyJ1IjoieXVyamlhIiwiYSI6ImNsY25ndWQyMTE2ZjYzdnJ5bDdzeXZ0Z28ifQ.oZobv-LbID3kkafdwvWZIA",
      legend_items: [],

      color_stairs: [
        "#fff176",
        "#ffeb3b",
        "#ffca28",
        "#ffb300",
        "#ff8f00",
        "#ff5722",
        "#e64a19",
        "#d84315",
        "#bf360c",
      ],
      data_steps_dict: {
        lossEuro: [1000, 4000, 10000, 16000, 30000, 50000, 80000, 100000],
        fatalities: [20, 50, 100, 200, 500, 1000, 2000, 5000],
      },
    };
  },
  methods: {
    updateLegend: function () {
      var data_steps = this.data_steps_dict[this.loss_type];
      var values = [
        ` [0, ${data_steps[0]})`,
        ` [${data_steps[0]}, ${data_steps[1]})`,
        ` [${data_steps[1]}, ${data_steps[2]})`,
        ` [${data_steps[2]}, ${data_steps[3]})`,
        ` [${data_steps[3]}, ${data_steps[4]})`,
        ` [${data_steps[4]}, ${data_steps[5]})`,
        ` [${data_steps[5]}, ${data_steps[6]})`,
        ` [${data_steps[6]}, ${data_steps[7]})`,
        ` ${data_steps[7]} +`,
        " No data",
      ];
      var colors = this.color_stairs;
      colors.push("white");

      this.legend_items = [];
      for (var i = 0; i < values.length; i++) {
        var value = values[i];
        var color = colors[i];
        this.legend_items.push({ value, color });
      }
    },

    updateData: function () {
      this.updateLegend();
      // Update data
      var data_steps = this.data_steps_dict[this.loss_type];
      var color_stairs = this.color_stairs;
      this.map.setPaintProperty("countries-layer", "fill-color", [
        "case",
        ["==", ["get", this.loss_type], null],
        "white",
        [
          "step",
          ["get", this.loss_type],
          color_stairs[0],
          data_steps[0],
          color_stairs[1],
          data_steps[1],
          color_stairs[2],
          data_steps[2],
          color_stairs[3],
          data_steps[3],
          color_stairs[4],
          data_steps[4],
          color_stairs[5],
          data_steps[5],
          color_stairs[6],
          data_steps[6],
          color_stairs[7],
          data_steps[7],
          color_stairs[8],
        ],
      ]);
      console.info("update color: " + this.loss_type);
    },
  },

  mounted() {
    mapboxgl.accessToken = this.accessToken;

    var bounds = [
      [-60, 20], // Southwest coordinates
      [50, 70], // Northeast coordinates
    ];

    var map = new mapboxgl.Map({
      container: "globalMap",
      style: "mapbox://styles/mapbox/light-v11",
      center: [7, 50],
      zoom: 3.9,
      maxBounds: bounds, // Sets bounds as max
      projection: "lambertConformalConic",
    });

    var hoveredStateId = null;

    map.on("load", () => {
      // Add a source for the country polygons.
      map.addSource("countries", {
        type: "geojson",
        data: this.data_dir,
        generateId: true, // This ensures that all features have unique IDs
      });

      // Add a layer showing the country polygons.
      map.addLayer(
        {
          id: "countries-layer",
          type: "fill",
          source: "countries",
          paint: {},
        },
        "waterway-label"
      );
      this.updateData();

      // Create a popup, but don't add it to the map yet.
      var popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false,
      });
      // Change the cursor to a pointer when the mouse is over the states layer.
      // Update popup window on hover.
      map.on("mousemove", "countries-layer", (e) => {
        map.getCanvas().style.cursor = "pointer";
        var popupInfo;

        var _type_text = this.total_or_per_cap;
        if ("per_capita" === _type_text) {
          _type_text = "per capita";
        }
        var _emission_text = this.emission_type;
        if ("co2" === _emission_text) {
          _emission_text = "CO<sub>2</sub>";
        } else {
          _emission_text = "GHGs";
        }

        if (
          !isNaN(
            e.features[0].properties[
              this.emission_type +
                "_" +
                this.total_or_per_cap +
                "_" +
                this.sliderValue
            ]
          )
        ) {
          popupInfo =
            "<strong>" +
            e.features[0].properties.name +
            "</strong> " +
            "<br/>" +
            _type_text +
            " " +
            _emission_text +
            " emission" +
            " in " +
            this.sliderValue +
            ":" +
            "<br />" +
            e.features[0].properties[
              this.emission_type +
                "_" +
                this.total_or_per_cap +
                "_" +
                this.sliderValue
            ].toFixed(3) +
            " " +
            this.emission_unit;
        } else {
          popupInfo =
            "<strong>" +
            e.features[0].properties.name +
            "</strong>" +
            ": No data";
        }
        popup.setLngLat(e.lngLat).setHTML(popupInfo).addTo(map);
        if (e.features.length > 0) {
          if (hoveredStateId !== null) {
            map.setFeatureState(
              { source: "countries", id: hoveredStateId },
              { hover: false }
            );
          }
          hoveredStateId = e.features[0].id;
          map.setFeatureState(
            { source: "countries", id: hoveredStateId },
            { hover: true }
          );
        }
      });
      // Change the cursor back to a pointer and remove popup when the mouse leaves.
      map.on("mouseleave", "countries-layer", function () {
        map.getCanvas().style.cursor = "";
        popup.remove();
        if (hoveredStateId !== null) {
          map.setFeatureState(
            { source: "countries", id: hoveredStateId },
            { hover: false }
          );
        }
        hoveredStateId = null;
      });
    });

    // Disable map zoom in/out using scroll
    map.scrollZoom.disable();
    // Disable map rotation using right click + drag
    map.dragRotate.disable();
    // Disable map rotation using touch rotation gesture
    map.touchZoomRotate.disableRotation();
    // Add zoom and rotation controls to the map.
    map.addControl(new mapboxgl.NavigationControl());

    this.map = map;
  },
};
</script>

<style scoped lang="scss">
/*Container bottom left*/
.container {
  position: relative;
  width: max(1000px, 80vw);
  height: max(800px, 70vh);
  margin: 0 auto;
}

#globalMap {
  //   position: absolute;
  width: 85%;
  //width: 1300px;
  height: 100%;
}

.map-overlay {
  position: absolute;
  bottom: 5px;
  left: 5px;
  background: rgba(255, 255, 255, 0.8);
  font-family: Arial, sans-serif;
  overflow: auto;
  border-radius: 3px;
  overflow-y: hidden;
}

#legend {
  padding: 10px;
  //   padding-left: 20px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 20px;
  height: 400px;
  //margin-bottom: 0px;
  width: 250px;
}

.legend-key {
  display: inline-block;
  border-radius: 20%;
  width: 10px;
  height: 10px;
  margin-left: 20px;
  //   padding-left: 20px;
}

.map-overlay input {
  background-color: transparent;
  display: inline-block;
  width: 100%;
  position: relative;
  margin: 0;
  cursor: ew-resize;
}
</style>
