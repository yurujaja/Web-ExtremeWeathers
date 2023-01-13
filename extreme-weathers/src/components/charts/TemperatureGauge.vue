<template>
  <div class="gauge-text">
    <div>Historical Average Temperatures of July in Paris</div>
    <br />
    <div>Year: {{ current_year }}</div>

    <div
      ref="gauge"
      style="
        height: 350%;
        /* width: 300%; */
        position: relative;
        margin-right: 4%;
        margin-left: 4%;
        /* padding-left: 4%;
        padding-right: 5%; */
      "
    ></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  name: "TemperatureGauge",
  components: {},
  data() {
    return {
      current_year: "2002",
    };
  },
  setup() {
    return {};
  },
  mounted() {
    var myChart = echarts.init(this.$refs["gauge"]);
    var option;
    option = {
      // title: {
      //   text: "Historical Average Temperatures of July in Paris",
      //   top: "top",
      //   left: "center",
      // },
      series: [
        {
          type: "gauge",
          center: ["50%", "60%"],
          startAngle: 200,
          endAngle: -20,
          min: 0,
          max: 60,
          splitNumber: 12,
          itemStyle: {
            color: "#FFAB91",
          },
          progress: {
            show: true,
            width: 30,
          },
          pointer: {
            show: false,
          },
          axisLine: {
            lineStyle: {
              width: 30,
            },
          },
          axisTick: {
            distance: -45,
            splitNumber: 5,
            lineStyle: {
              width: 2,
              color: "#999",
            },
          },
          splitLine: {
            distance: -52,
            length: 14,
            lineStyle: {
              width: 3,
              color: "#999",
            },
          },
          axisLabel: {
            distance: -20,
            color: "#999",
            fontSize: 20,
          },
          anchor: {
            show: false,
          },
          title: {
            show: false,
          },
          detail: {
            valueAnimation: true,
            width: "60%",
            lineHeight: 40,
            borderRadius: 8,
            offsetCenter: [0, "-15%"],
            fontSize: 45,
            fontWeight: "bolder",
            formatter: "{value} °C",
            color: "inherit",
          },
          data: [
            {
              value: 21.71,
            },
          ],
        },
        {
          type: "gauge",
          center: ["50%", "60%"],
          startAngle: 200,
          endAngle: -20,
          min: 0,
          max: 60,
          itemStyle: {
            color: "#FD7347",
          },
          progress: {
            show: true,
            width: 8,
          },
          pointer: {
            show: false,
          },
          axisLine: {
            show: false,
          },
          axisTick: {
            show: false,
          },
          splitLine: {
            show: false,
          },
          axisLabel: {
            show: false,
          },
          detail: {
            show: false,
          },
          data: [
            {
              value: 21.71,
            },
          ],
        },
      ],
    };
    var curTempIndex = -1;
    const tempArrayJuly = [21.71, 26.21, 26.57, 29.57, 30.86];
    const yearsArray = ["2000", "2005", "2010", "2015", "2022"];
    setInterval(() => {
      ++curTempIndex;
      if (curTempIndex >= tempArrayJuly.length) {
        curTempIndex = 0;
      }
      this.current_year = yearsArray[curTempIndex];
      myChart.setOption({
        series: [
          {
            data: [
              {
                value: tempArrayJuly[curTempIndex],
              },
            ],
          },
          {
            data: [
              {
                value: tempArrayJuly[curTempIndex],
              },
            ],
          },
        ],
      });
    }, 1500);

    myChart.setOption(option);
  },
};
</script>

<style>
.gauge-text {
  text-align: center;
  color: #2d4856;
  font-size: 130%;
  font-weight: bold;
  margin-left: 35%;
}
</style>
