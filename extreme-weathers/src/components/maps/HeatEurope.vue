<template>
  <div class="container justify-center items-center content-center">
    <div id="heatMap"></div>

    <div class="map-overlay" id="legend">
      <div class="legend-title">Extreme temperatures over 40 ℃</div>
      <q-space class="q-ma-sm" />
      <label id="year">Year: from 1980-2022</label>
    </div>
  </div>
</template>
<!-- <script src="https://api.mapbox.com/mapbox-gl-js/v2.12.0/mapbox-gl.js"></script> -->
<script>
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";

export default {
  name: "HeatEuropeMap",
  data() {
    return {
      data_path: "data/europe_heat_events.geojson",
      map: "",
      accessToken:
        "pk.eyJ1IjoieXVyamlhIiwiYSI6ImNsY25ndWQyMTE2ZjYzdnJ5bDdzeXZ0Z28ifQ.oZobv-LbID3kkafdwvWZIA",
    };
  },
  methods: {},

  mounted() {
    mapboxgl.accessToken = this.accessToken;
    const size = 200;
    // This implements `StyleImageInterface`
    // to draw a pulsing dot icon on the map.
    const pulsingDot = {
      width: size,
      height: size,
      data: new Uint8Array(size * size * 4),

      // When the layer is added to the map,
      // get the rendering context for the map canvas.
      onAdd: function () {
        const canvas = document.createElement("canvas");
        canvas.width = this.width;
        canvas.height = this.height;
        this.context = canvas.getContext("2d");
      },

      // Call once before every frame where the icon will be used.
      render: function () {
        const duration = 1000;
        const t = (performance.now() % duration) / duration;

        const radius = (size / 2) * 0.3;
        const outerRadius = (size / 2) * 0.7 * t + radius;
        const context = this.context;

        // Draw the outer circle.
        context.clearRect(0, 0, this.width, this.height);
        context.beginPath();
        context.arc(
          this.width / 2,
          this.height / 2,
          outerRadius,
          0,
          Math.PI * 2
        );
        context.fillStyle = `rgba(255, 200, 200, ${1 - t})`;
        context.fill();

        // Draw the inner circle.
        context.beginPath();
        context.arc(this.width / 2, this.height / 2, radius, 0, Math.PI * 2);
        context.fillStyle = "rgba(255, 100, 100, 1)";
        context.strokeStyle = "white";
        context.lineWidth = 2 + 4 * (1 - t);
        context.fill();
        context.stroke();

        // Update this image's data with data from the canvas.
        this.data = context.getImageData(0, 0, this.width, this.height).data;

        // Continuously repaint the map, resulting
        // in the smooth animation of the dot.
        map.triggerRepaint();

        // Return `true` to let the map know that the image was updated.
        return true;
      },
    };
    var bounds = [
      [-58, 16], // Southwest coordinates
      [50, 65], // Northeast coordinates
    ];

    var map = new mapboxgl.Map({
      container: "heatMap",
      style: "mapbox://styles/mapbox/dark-v11",
      center: [10, 48],
      zoom: 4.2,
      maxBounds: bounds, // Sets bounds as max
      projection: "lambertConformalConic",
    });

    var hoveredStateId = null;

    map.on("load", () => {
      map.addImage("pulsing-dot", pulsingDot, { pixelRatio: 4 });
      // Add a source for the country polygons.
      map.addSource("heat-dot-point", {
        type: "geojson",
        data: this.data_path,
        generateId: true, // This ensures that all features have unique IDs
      });

      // Add a layer showing the country polygons.
      map.addLayer(
        {
          id: "heat-dot-layer",
          type: "circle",
          source: "heat-dot-point",
          // layout: {
          //   "icon-image": "pulsing-dot",
          // },
          paint: {
            "circle-color": "#EC4825",
            "circle-opacity": 0.75,
            "circle-radius": [
              "interpolate",
              ["linear"],
              ["get", "heat_events"],
              1,
              8,
              2,
              12,
              3,
              18,
              4,
              22,
              5,
              28,
            ],
          },
        },
        "waterway-label"
      );

      // Create a popup, but don't add it to the map yet.
      var popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false,
      });
      // Change the cursor to a pointer when the mouse is over the states layer.
      // Update popup window on hover.
      map.on("mousemove", "heat-dot-layer", (e) => {
        map.getCanvas().style.cursor = "pointer";
        var popupInfo =
          e.features[0].properties.name +
          "<br/>" +
          "Number of events:  " +
          e.features[0].properties.heat_events;

        popup.setLngLat(e.lngLat).setHTML(popupInfo).addTo(map);
        if (e.features.length > 0) {
          if (hoveredStateId !== null) {
            map.setFeatureState(
              { source: "heat-dot-point", id: hoveredStateId },
              { hover: false }
            );
          }
          hoveredStateId = e.features[0].id;
          map.setFeatureState(
            { source: "heat-dot-point", id: hoveredStateId },
            { hover: true }
          );
        }
      });
      // Change the cursor back to a pointer and remove popup when the mouse leaves.
      map.on("mouseleave", "heat-dot-layer", function () {
        map.getCanvas().style.cursor = "";
        popup.remove();
        if (hoveredStateId !== null) {
          map.setFeatureState(
            { source: "heat-dot-point", id: hoveredStateId },
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
  width: max(800px, 60vw);
  height: max(800px, 60vh);
  margin: 0 auto;
}

#heatMap {
  //   position: absolute;
  width: 100%;
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
  top: 1%;
  border-radius: 3px;
  overflow-y: hidden;
}

#legend {
  padding: 10px;
  text-align: center;
  //   padding-left: 20px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 25px;
  height: 100px;
  //margin-bottom: 0px;
  width: 230px;
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

.legend-title {
  font-family: Arial, sans-serif;
  font-weight: bold;
  font-size: large;
}
</style>
