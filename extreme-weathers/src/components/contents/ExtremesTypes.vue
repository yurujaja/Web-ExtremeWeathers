<template>
  <div id="ways" style="padding: 5px; margin-left: 2%">
    <div class="row items-center q-pa-md">
      <div class="col">
        <q-card class="my-card, container" style="width: 95%">
          <q-img
            src="images/wildfires.jpg"
            :ratio="4 / 3"
            alt="art"
            class="image"
          >
            <div class="text-h6 absolute-top text-right">Wildfires</div>
          </q-img>
          <div class="overlay">
            <div class="text" style="text-align: left">
              Wildfires are occurring more often and burning larger areas in
              many parts of the world, such as the Amazon region, Australia,
              Siberia, and North America. More severe wildfires are likely to
              occur in a hotter and drier world, increasing the risk of
              wildfires in areas where fires were not previously common.
              Wildfires lead to more wildfires, because wildfires release large
              amounts of carbon into the atmosphere, further increasing global
              warming and amplifying climate change.
            </div>
          </div>
        </q-card>
      </div>

      <div class="col">
        <q-card class="my-card, container" style="width: 95%">
          <q-img src="images/storm.jpg" :ratio="4 / 3" alt="art" class="image">
            <div class="text-h6 absolute-top text-right">Storms</div>
          </q-img>
          <div class="overlay">
            <div class="text" style="text-align: left">
              As Earth’s climate warms, storms are predicted to happen more
              often and they will be stronger. Warming air is more unstable and
              has more winds and updrafts, creating more powerful thunderstorms,
              tornadoes, and blizzards. The ocean is also getting warmer and the
              extra heat can fuel big cyclones, which can create more extreme
              storm surges in coastal regions.
            </div>
          </div>
        </q-card>
      </div>
    </div>

    <div class="row items-center q-pa-md">
      <div class="col">
        <q-card class="my-card, container" style="width: 95%">
          <q-img
            src="images/drought.jpg"
            :ratio="4 / 3"
            alt="art"
            class="image"
          >
            <div class="text-h6 absolute-top text-right">
              Heatwaves and Droughts
            </div>
          </q-img>
          <div class="overlay">
            <div class="text" style="text-align: left">
              Heatwaves are usually defined as times when temperatures are much
              higher than expected over a few days in a row. Droughts occur when
              there is low water availability over a period of a few months or
              longer. Although droughts occur on different timescales and for
              different reasons, droughts and heatwaves are linked. During
              droughts, we are more likely to experience heatwaves because dry
              conditions favor warmer temperatures. Also, when a heatwave
              occurs, the heat can increase the rate at which moisture
              evaporates from vegetation and the land, increasing the severity
              of drought.
            </div>
          </div>
        </q-card>
      </div>

      <div class="col">
        <q-card class="my-card, container" style="width: 95%">
          <q-img src="images/floods.jpg" :ratio="4 / 3" alt="art" class="image">
            <div class="text-h6 absolute-top text-right">Floods</div>
          </q-img>
          <div class="overlay">
            <div class="text" style="text-align: left">
              While rain is a key part of Earth’s water cycle, extreme rain can
              cause too much water to fall in too short a time. We call rainfall
              “violent” when the ground receives more than 5 cm of water in 1 h.
              TExtreme rainfall brings severe risks to human health, the
              environment, and our economy. Impacts include flash flooding,
              landslides, damage to buildings and farmland, loss of livestock,
              and damage to lands and forests that increase soil erosion.
            </div>
          </div>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TypesCard",
};
</script>

<style scoped>
/* on hovering, shows text information over image card */
.container {
  position: relative;
  width: 50%;
}

.image {
  display: block;
  width: 100%;
  height: auto;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: 0.5s ease;
  background-color: rgba(45, 45, 45, 0.7);
}

.container:hover .overlay {
  opacity: 1;
}

.text {
  color: white;
  font-size: 18px;
  position: absolute;
  top: 50%;
  left: 50%;
  right: 0%;
  width: 90%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
}

a:link {
  color: white;
  background-color: transparent;
  text-decoration: underline;
}
</style>
