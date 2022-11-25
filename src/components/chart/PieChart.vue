<template>
  <div>
    <div>
      <div class="container">
        <div>
          <highcharts :options="chartOptions"></highcharts>
        </div>
      </div>
    </div>
    <p v-if="subtitle == 'Online'">{{ subtitle }} {{ onlineInfo.total }}</p>
    <p v-if="subtitle == 'Offline'">{{ subtitle }} {{ offlineInfo.total }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, watch } from "vue";
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
    selectListsview: {
      type: Object,
      default: () => {
        return {};
      },
    },
    onlineInfo: {
      type: Object,
      default: () => {
        return {};
      },
    },
    offlineInfo: {
      type: Object,
      default: () => {
        return {};
      },
    },

    subtitle: String,
  },
  setup(props) {
    const online = reactive({
      error: props.onlineInfo.error,
      warning: props.onlineInfo.warning,
      normal: props.onlineInfo.normal,
    });

    watch(props, () => {
      console.log("online!!", props.onlineInfo); //watch로 rerender
      console.log("offline!!", props.offlineInfo); //watch로 rerender
    });
    let data: any = [];
    // if (props.onlineInfo) {
    data = [
      ["Error", props.onlineInfo.error],
      ["Warning", props.onlineInfo.warning],
      ["Normal", props.onlineInfo.normal],
    ];
    // }
    // if (props.offlineInfo) {
    data = [
      ["Error", props.offlineInfo.error],
      ["Warning", props.offlineInfo.warning],
      ["Normal", props.offlineInfo.normal],
    ];
    // }

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
        colors: ["red", "yellow", "blue"],
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
              props.onlineInfo.error
                ? ["Error", props.onlineInfo.error]
                : ["Error", props.offlineInfo?.error],
              props.onlineInfo.warning
                ? ["Warning", props.onlineInfo?.warning]
                : ["Warning", props.offlineInfo?.warning],
              props.onlineInfo.normal
                ? ["Normal", props.onlineInfo?.normal]
                : ["Normal", props.offlineInfo?.normal],
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
