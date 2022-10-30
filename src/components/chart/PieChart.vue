<template>
  <div>
    <div class="container">
      <div>
        <highcharts :options="chartOptions"></highcharts>
      </div>
      <!-- <h3>hi{{ chartData }}</h3> -->
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Chart } from "highcharts-vue";

export default defineComponent({
  name: "PieChart",
  components: {
    highcharts: Chart,
  },
  props: {
    chartData: {
      type: Object,
      default: () => {
        return {};
      },
    },
    // selectList: {
    //   type: Object,
    //   default: () => {
    //     return {};
    //   },
    // },
  },
  setup(props: object) {
    console.log(props);
    return {
      chartOptions: {
        title: {
          text: "",
        },
        tooltip: {
          pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>",
        },
        plotOptions: {
          pie: {
            dataLabels: {
              enabled: true,
            },
          },
        },
        colors: ["red", "yellow", "blue", "orange"],
        series: [
          {
            type: "pie",
            name: "",
            innerSize: "0%",
            data: [
              ["1", 10.0],
              ["2", 20.0],
              ["3", 30.0],
              ["4", 40.0],
            ],
          },
        ],
      },
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
}
</style>
