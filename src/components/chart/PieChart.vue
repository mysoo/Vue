<template>
  <div class="container">
    <div class="box">
      <p>Product</p>
      <p>Installed Last Week</p>
    </div>
  </div>

  <div>
    <highcharts :options="chartOptions"></highcharts>
  </div>
  <h3>{{ chartData }}</h3>
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
    // chartOptions: String,
  },
  data() {
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
              enabled: false,
            },
          },
        },
        colors: ["red", "yellow", "blue", "orange"],
        series: [
          {
            type: "pie",
            name: "",
            innerSize: "45%",
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
}
.box {
  border-bottom: 2px solid rgb(160, 159, 159);
  width: 90%;
  display: flex;
  p {
    margin: 2% 2% 2% 0;
    font-weight: bold;
  }
}
</style>
