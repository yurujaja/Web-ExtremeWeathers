<template>
  <div class="row items-center" style="margin-top: 5%">
    <div class="col" style="margin-left: 5%; margin-right: 5%">
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
      <q-img src="images/global_warming_forecast.png" :fit="contain"></q-img>
      <div></div>
    </div>
  </div>
  <div class="row items-center" style="margin-top: 2%">
    <div class="col" style="margin-left: 5%">
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
  <div style="margin-top: 5%; margin-bottom: 5%">
    <strong class="text-primary" style="font-size: 250%">
      What Should be Done?
    </strong>
    <q-space class="q-ma-sm" />
    <LimitWidth
      ><div class="text-body1">
        <p>
          There is no singular solution to navigating the next wave of
          challenges. But a focus on proven and tested intervention strategies
          is imperative. To alleviate the many climatic challenges, cities must
          design with mitigation and adaptation in mind. Below are a few
          recommendations that tackle different intervention categories.
        </p>
      </div></LimitWidth
    >

    <div class="row justify-center">
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Building and urban planning
          </div>
        </div>
        <div class="content">
          <p>
            Building orientation , shading canyons , lightreflecting materials ,
            insulation in building construction
            <q-space class="q-ma-sm" />
            Shading trees , green roofs , parks and outdoor vegetation
            <q-space class="q-ma-sm" />
            Shaded pathways and outdoor spaces with water features
            <q-space class="q-ma-sm" />
            Urban planning regulations to reinforce the above strateqies
          </p>
        </div>
      </div>
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Cooling technologies & solutions
          </div>
        </div>
        <div class="content">
          <p>
            Low-tech solutions including fans , desert coolersand evaporative
            technoloaies and natural ventilation use
            <q-space class="q-ma-sm" />
            Low-energy use devices with high COPS (Coefficients of Performance )
            <q-space class="q-ma-sm" />
            Electricity production and renewable energy systems (PVs)
            <q-space class="q-ma-sm" />
            District cooling
          </p>
        </div>
      </div>
      <div class="col-12 col-md-3">
        <div class="title text-center">
          <div class="text-h5 text-bold title-text">
            Legislation & education
          </div>
        </div>
        <div class="content">
          <p>
            Programs in place for vulnerable populations with no access to
            electricity and means of cooling
            <q-space class="q-ma-sm" />
            Risk management on district level
            <q-space class="q-ma-sm" />
            Heat mitigation awarness and the provision of cooling centers in
            urban city centers
            <q-space class="q-ma-sm" />
            Local laws and regulations to finance climate-driven retrofits
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LimitWidth from "../utils/LimitWidth.vue";
export default {
  name: "OutlookSession",
  components: {
    LimitWidth,
  },
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
  text-align: center;
}
.content {
  margin: 5px;
  padding: 15px;
  font-size: 145%;
  text-align: left;
}
</style>
