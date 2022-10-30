<template>
  <div>
    <div>
      <div class="container">
        <div>
          <highcharts :options="chartOptions"></highcharts>
        </div>
      </div>
    </div>
    <p>{{ subtitle }}</p>
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
    selectedList: {
      type: Object,
      default: () => {
        return {};
      },
    },
    subtitle: String,
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
        credits: {
          //remove mark
          enabled: false,
        },
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
  min-width: 400px;
}
p {
  font-weight: bold;
}
</style>
