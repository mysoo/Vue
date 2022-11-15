<template>
  <div>
    <div>
      <div class="container">
        <div>
          <highcharts :options="chartOptions"></highcharts>
        </div>
      </div>
    </div>
    <p>{{ subtitle }} {{ onlinetotal }}</p>
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
    onlineSelectList: {
      type: Object,
      default: () => {
        return {};
      },
    },
    offlineSelectList: {
      type: Object,
      default: () => {
        return {};
      },
    },
    onlinetotal: {
      type: Object,
      default: () => {
        return {};
      },
    },
    subtitle: String,
  },
  setup(props) {
    console.log("props_on", props.onlineSelectList);
    console.log("props_off", props.offlineSelectList);
    console.log("onlinetotal", props.onlinetotal);
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
            showInLegend: true,
          },
        },
        colors: ["red", "yellow", "blue", "orange"],
        credits: {
          //remove mark
          enabled: false,
        },
        accessibility: {
          enabled: false,
        },
        legend: {
          //범례
          layout: "horizontal",
          align: "center",
          verticalAlign: "top",
          x: -4,
          y: -2,
          itemMarginTop: 30, //범례 margin top 지정(bottom도 존재.)
          symbolHeight: 10,
          symbolWidth: 10,
          // symbolPadding: 5,
          symbolRadius: 10,
          itemStyle: {
            color: "#444",
            fontSize: "15px",
            fontWeight: "normal",
          },
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

  @at-root p {
    font-weight: bold;
  }
}
</style>
