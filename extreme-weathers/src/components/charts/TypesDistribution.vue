<template>
  <div>
    <div ref="piechart" style="height: 700px"></div>
  </div>
</template>

<script>
import { ref } from "vue";
import * as echarts from "echarts";

export default {
  name: "TypesPieChart",
  components: {},
  setup() {
    return {};
  },
  mounted() {
    var myChart = echarts.init(this.$refs["piechart"]);

    var option;
    option = {
      title: {
        text: "The distribution of extreme weather types",
        top: "bottom",
        left: "center",
      },
      tooltip: {
        trigger: "item",
      },
      legend: {
        orient: "vertical",
        left: "left",
      },
      series: [
        {
          name: "Access From",
          type: "pie",
          radius: "50%",
          data: [
            { value: 546, name: "Storms" },
            { value: 444, name: "Floods" },
            { value: 62, name: "Wildfires" },
            { value: 53, name: "Heatwaves" },
          ],
          emphasis: {
            itemStyle: {
              shadowBlur: 10,
              shadowOffsetX: 0,
              shadowColor: "rgba(0, 0, 0, 0.5)",
            },
          },
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
