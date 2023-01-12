<template>
  <div class="row items-center" style="margin-top: 5%">
    <div class="col">
      <div
        class="text-body1"
        style="margin-right: 35%; margin-left: 10%; width: 80%"
      >
        <p style="text-align: center; font-size: 120%">
          <strong
            >How close are we to reaching a global warming of 1.5˚C?</strong
          >
        </p>
        <br />
        <p>
          Reaching 1.5˚C of global warming - a limit agreed under the Paris
          agreement - may feel like a very distant reality, but it might be
          closer than you think. Experts suggest it is likely to happen between
          2030 and the early 2050s. Figure on the right shows where we are now
          and how soon we would reach the limit if the warming continued at
          today’s pace.
        </p>
        <q-space></q-space>
        <p></p>
        <q-space></q-space>
        <p></p>
      </div>
    </div>
    <div class="col">
      <q-img src="images/global_warming_forecast.png" width="100%"></q-img>
      <div>
        <!-- <small
          ><a
            href="https://cds.climate.copernicus.eu/cdsapp#!/software/app-c3s-global-temperature-trend-monitor?tab=app"
            >source</a
          ></small
        > -->
      </div>
    </div>
  </div>
  <div class="row items-center" style="margin-top: 5%">
    <div class="col">
      <iframe
        width="800"
        height="550"
        src="https://www.youtube.com/embed/5wYFFlSuauQ"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen
      ></iframe>
    </div>
    <div class="col">
      <div
        class="text-body1"
        style="margin-right: 35%; margin-left: 10%; width: 80%"
      >
        <p style="text-align: center; font-size: 120%">
          <strong>Future weather forecast for the year 2050</strong>
        </p>
        <br />
        <p>
          The future climate could be determined by the level of emissions in
          the coming years, so how could a weather forecast in 2050 look? This
          video illustrates that there could be more extreme heat events and
          changes to the coastline. As well as rising temperatures, the video
          outlines some of the other physical changes in the climate we can
          expect and how they might impact business and industry.
        </p>
        <q-space></q-space>
        <p></p>
        <q-space></q-space>
        <p></p>
      </div>
    </div>
  </div>

  <q-space class="q-ma-sm" />
  <q-space class="q-ma-sm" />
  <div style="margin-top: 5%">
    <strong class="text-primary" style="font-size: 250%">
      What can be done?
    </strong>
    <div class="row justify-center">
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Vaccinate and co-operate
          </div>
        </div>
        <div class="content text-body2">
          Increase vaccine production and accelerate vaccination across the
          world.
          <q-space class="q-ma-sm" />
          Reduce barriers to the supply chain of vaccine components and
          materials.
          <q-space class="q-ma-sm" />
          Improve cooperation between countries and expand medical and financial
          resources to help developing regions.
        </div>
      </div>
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Support people and business
          </div>
        </div>
        <div class="content text-body2">
          Offer income support for workers in hard-hit sectors. Adapt policies
          according to economic and health developments to transition from
          emergency to recovery.
          <q-space class="q-ma-sm" />
          Support companies affected by restrictions, preferably through grants
          and equity rather than debt.
          <q-space class="q-ma-sm" />
          Help the low skilled and the vulnerable, improve training schemes and
          access to the labour market.
        </div>
      </div>
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Prepare for a sustainable recovery
          </div>
        </div>
        <div class="content text-body2">
          Avoid removing government stimulus funding too early.
          <q-space class="q-ma-sm" />
          Invest in healthcare, cleaner infrastructure and digital technology to
          foster a transition to a more resilient and sustainable economy.
          <q-space class="q-ma-sm" />
          Focus on structural reforms that can boost medium-term growth in
          productivity and employment.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "OutlookSession",
  components: {},
};
</script>

<style>
img {
  max-width: 90vw;
}

.title {
  background-color: #2d4856;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  margin: 5px;
  padding: 10px;
}
.title-text {
  color: white;
}
.content {
  margin: 5px;
  padding: 10px;
}
</style>
