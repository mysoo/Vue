<template>
  <div class="container">
    <div class="box">
      <div><CheckBox @selectList="selectListsview" /></div>
      <div class="container">
        <div class="titlebox">
          <p>Product</p>
          <p class="values">{{ totalProduct.initTotalV }}</p>

          <p>Installed Last Week</p>
          <p class="values">{{ installedLastWeek.initinstalledV }}</p>
        </div>
      </div>
      <div class="chartbox">
        <div>
          <PieChart
            :subtitle="onLine"
            :chartData="chartData"
            :onlineInfo="onlineInfo"
          />
        </div>

        <div>
          <PieChart
            :subtitle="offLine"
            :chartData="chartData"
            :offlineInfo="offlineInfo"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import CheckBox from "../common/CheckBox.vue";
import PieChart from "../chart/PieChart.vue";

export default defineComponent({
  name: "ChartMain",
  components: { CheckBox, PieChart },
  props: {
    chartData: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },

  setup(props) {
    const onLine = "Online";
    const offLine = "Offline";
    const add = (arr: number[]) =>
      arr.reduce((a: number, b: number) => a + b, 0);

    const initProduct = props.chartData.map((i: any) => {
      return i.totalCount;
    });

    const initInstalled = props.chartData.map((i: any) => {
      return i.lastWeekCount;
    });

    const initOnlineTotal = props.chartData.map((i: any) => {
      return i.onlineErrorCount + i.onlineNormalCount + i.onlineWarningCount;
    });
    const initOfflineTotal = props.chartData.map((i: any) => {
      return i.offlineErrorCount + i.offlineNormalCount + i.offlineWarningCount;
    });
    const initOnlineNormal = props.chartData.map((i: any) => {
      return i.onlineNormalCount;
    });
    const initOnlineWarning = props.chartData.map((i: any) => {
      return i.onlineWarningCount;
    });
    const initOnlineError = props.chartData.map((i: any) => {
      return i.onlineErrorCount;
    });
    const initOfflineNormal = props.chartData.map((i: any) => {
      return i.offlineNormalCount;
    });
    const initOfflineWarning = props.chartData.map((i: any) => {
      return i.offlineWarningCount;
    });
    const initOfflineError = props.chartData.map((i: any) => {
      return i.offlineErrorCount;
    });
    const initTotalV = add(initProduct);
    const initinstalledV = add(initInstalled);
    const initOnlineTotalV = add(initOnlineTotal);
    const initOfflineTotalV = add(initOfflineTotal);
    const initOnlineTotalN = add(initOnlineNormal);
    const initOnlineTotalW = add(initOnlineWarning);
    const initOnlineTotalE = add(initOnlineError);
    const initOfflineTotalN = add(initOfflineNormal);
    const initOfflineTotalW = add(initOfflineWarning);
    const initOfflineTotalE = add(initOfflineError);

    const totalProduct = reactive({ initTotalV: initTotalV });
    const installedLastWeek = reactive({ initinstalledV: initinstalledV });
    const totalValues = reactive({ value: [] }); //selectLists와 chartData 교집합
    const onlineInfo = reactive({
      value: 0,
      total: initOnlineTotalV,
      normal: initOnlineTotalN,
      warning: initOnlineTotalW,
      error: initOnlineTotalE,
    });
    const offlineInfo = reactive({
      value: 0,
      total: initOfflineTotalV,
      normal: initOfflineTotalN,
      warning: initOfflineTotalW,
      error: initOfflineTotalE,
    });

    // selectList데이터를 가공해서 piechart에 전달
    const selectListsview = (selectLists: string[]) => {
      console.log("selectLists!!", selectLists);

      totalProduct.initTotalV = 0;
      installedLastWeek.initinstalledV = 0;
      onlineInfo.value = 0;
      onlineInfo.total = 0;
      onlineInfo.normal = 0;
      onlineInfo.warning = 0;
      onlineInfo.error = 0;
      offlineInfo.value = 0;
      offlineInfo.total = 0;
      offlineInfo.normal = 0;
      offlineInfo.warning = 0;
      offlineInfo.error = 0;

      totalValues.value = props.chartData.map((i: any) => {
        if (selectLists.includes(i.countryCd)) {
          totalProduct.initTotalV += i.totalCount;
          installedLastWeek.initinstalledV += i.lastWeekCount;
          onlineInfo.value =
            i.onlineErrorCount + i.onlineNormalCount + i.onlineWarningCount;
          offlineInfo.value =
            i.offlineErrorCount + i.offlineNormalCount + i.offlineWarningCount;

          onlineInfo.total += onlineInfo.value;
          offlineInfo.total += offlineInfo.value;
          // console.log("onlineInfo", onlineInfo.total);
          // console.log(i.countryCd, i.onlineNormalCount);
          onlineInfo.normal += i.onlineNormalCount;
          onlineInfo.warning += i.onlineWarningCount;
          onlineInfo.error += i.onlineErrorCount;
          offlineInfo.normal += i.offlineNormalCount;
          offlineInfo.warning += i.offlineWarningCount;
          offlineInfo.error += i.offlineErrorCount;
        }
      });
    };

    return {
      onLine,
      offLine,
      selectListsview,
      totalProduct,
      installedLastWeek,
      onlineInfo,
      offlineInfo,
    };
  },
});
</script>

<style scoped lang="scss">
.container {
  margin-top: 40px;
  display: flex;
  justify-content: center;
  .box {
    box-sizing: border-box;
    background-color: #fff;
    min-height: 300px;
    width: 85%;
    box-shadow: 3px 3px 3px 3px #7aade0;
    border-radius: 10px;
    padding: 40px;
    .chartbox {
      display: flex;
      flex-direction: row;
      justify-content: space-around;
    }
  }
}
.titlebox {
  box-sizing: border-box;
  border-bottom: 2px solid rgb(160, 159, 159);
  width: 90%;
  display: flex;

  p {
    margin: 2% 2% 2% 0;
    font-weight: bold;
  }
  .values {
    color: #0c70f2;
  }
}
</style>
