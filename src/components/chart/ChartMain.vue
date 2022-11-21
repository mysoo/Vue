<template>
  <div class="container">
    <div class="box">
      <div><CheckBox @selectList="selectListsview" /></div>
      <div class="container">
        <div class="titlebox">
          <p>Product</p>
          <p class="values">{{ totalProduct }}</p>

          <p>Installed Last Week</p>
          <p class="values">{{ installedLastWeek }}</p>
        </div>
      </div>
      <div class="chartbox">
        <div>
          <PieChart :subtitle="onLine" :chartData="chartData" />
        </div>

        <div>
          <PieChart :subtitle="offLine" :chartData="chartData" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, Ref, computed } from "vue";
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

    const initTotalV = add(initProduct);
    const initinstalledV = add(initInstalled);

    let totalProduct = ref(initTotalV);
    let installedLastWeek = ref(initinstalledV);
    let totalValues = ref([]); //selectLists와 chartData 교집합

    const selectListsview = (selectLists: string[]) => {
      console.log("selectLists!!", selectLists);

      totalProduct.value = 0;
      installedLastWeek.value = 0;

      totalValues.value = props.chartData.map((i: any) => {
        if (selectLists.includes(i.countryCd)) {
          totalProduct.value += i.totalCount;
          installedLastWeek.value += i.lastWeekCount;
        }
      });

      // onlineSelectList.value = props.chartData.map((items: any) => {
      //   for (let i in selectLists) {
      //     if (items.countryCd == selectLists[i]) {
      //       onV =
      //         items.onlineErrorCount +
      //         items.onlineNormalCount +
      //         items.onlineWarningCount;

      //       console.log("it", onV);
      //     }
      //   }
      //   onlinetotal.value += onV;
      //   console.log("hhh", onlinetotal.value);
      //   return onlinetotal.value;
      // });

      return totalProduct.value, installedLastWeek.value;
    };

    // selectList데이터를 가공해서 piechart에 전달하기
    const offlineSelectList = props.chartData.map((items: object) => {
      return items;
    });

    return {
      onLine,
      offLine,
      selectListsview,
      // onlineSelectList,
      offlineSelectList,
      totalProduct,
      installedLastWeek,
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
