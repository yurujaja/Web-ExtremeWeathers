<template>
  <div>
    <div ref="chart" style="height: 700px"></div>
  </div>
</template>

<script>
import { ref } from "vue";
import * as echarts from "echarts";

export default {
  name: "CountryEventsChart",
  components: {},
  setup() {
    return {};
  },
  mounted() {
    var myChart = echarts.init(this.$refs["chart"]);
    var ROOT_PATH = "https://echarts.apache.org/examples";
    const weatherIcons = {
      Wildfires: "images/wildfire-icon.png",
      heatwaves: "images/heat-icon.png",
      Storms: ROOT_PATH + "/data/asset/img/weather/showers_128.png",
      Floods: "images/floods-icon.png",
    };
    const seriesLabel = {
      show: true,
    };
    var option;
    option = {
      title: {
        text: "The extreme events occurrence over countries from 2002 to 2022",
        top: "bottom",
        left: "center",
      },
      tooltip: {
        trigger: "axis",
        axisPointer: {
          type: "shadow",
        },
      },
      legend: {
        data: ["USA", "China", "India"],
      },
      grid: {
        left: 100,
      },
      toolbox: {
        show: true,
        feature: {
          saveAsImage: {},
        },
      },
      xAxis: {
        type: "value",
        name: "Days",
        axisLabel: {
          formatter: "{value}",
        },
      },
      yAxis: {
        type: "category",
        inverse: true,
        data: ["Storms", "Floods", "Wildfires", "heatwaves"],
        axisLabel: {
          formatter: function (value) {
            return "{" + value + "| }\n{value|" + value + "}";
          },
          margin: 20,
          rich: {
            value: {
              lineHeight: 30,
              align: "center",
            },
            Wildfires: {
              height: 40,
              align: "center",
              backgroundColor: {
                image: weatherIcons.Wildfires,
              },
            },
            Storms: {
              height: 40,
              align: "center",
              backgroundColor: {
                image: weatherIcons.Storms,
              },
            },
            heatwaves: {
              height: 40,
              align: "center",
              backgroundColor: {
                image: weatherIcons.heatwaves,
              },
            },
            Floods: {
              height: 40,
              align: "center",
              backgroundColor: {
                image: weatherIcons.Floods,
              },
            },
          },
        },
      },
      series: [
        {
          name: "USA",
          type: "bar",
          data: [287, 94, 56, 17],
          label: seriesLabel,
          markPoint: {
            symbolSize: 1,
            symbolOffset: [0, "50%"],
            label: {
              formatter: "{a|{a}\n}{b|{b} }{c|{c}{d|{d}}",
              backgroundColor: "rgb(242,242,242)",
              borderColor: "#aaa",
              borderWidth: 1,
              borderRadius: 4,
              padding: [4, 10],
              lineHeight: 26,
              // shadowBlur: 5,
              // shadowColor: '#000',
              // shadowOffsetX: 0,
              // shadowOffsetY: 1,
              position: "right",
              distance: 20,
              rich: {
                a: {
                  align: "center",
                  color: "#fff",
                  fontSize: 18,
                  textShadowBlur: 2,
                  textShadowColor: "#000",
                  textShadowOffsetX: 0,
                  textShadowOffsetY: 1,
                  textBorderColor: "#333",
                  textBorderWidth: 2,
                },
                b: {
                  color: "#333",
                },
                c: {
                  color: "#ff8811",
                  textBorderColor: "#000",
                  textBorderWidth: 1,
                  fontSize: 22,
                },
                d: {
                  color: "#132",
                },
              },
            },
            // data: [
            //   { type: "max", name: "max days: " },
            //   { type: "min", name: "min days: " },
            // ],
          },
        },
        {
          name: "China",
          type: "bar",
          label: seriesLabel,
          data: [176, 183, 4, 20],
        },
        {
          name: "India",
          type: "bar",
          label: seriesLabel,
          data: [83, 167, 2, 16],
        },
      ],
    };
    myChart.setOption(option);
    window.addEventListener("resize", function () {
      myChart.resize();
    });
  },
};
</script>

<style scoped></style>
