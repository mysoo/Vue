<template>
  <div class="container">
    <div class="box">
      <div><CheckBox @selectList="selectListsview" /></div>
      <div class="container">
        <div class="titlebox">
          <p>Product</p>
          <p>Installed Last Week</p>
        </div>
      </div>
      <div class="chartbox">
        <div>
          <PieChart
            :subtitle="onLine"
            :chartData="chartData"
            :selectedList="onlineSelectList"
            :onlinetotal="onlineSelectList"
          />
        </div>

        <div>
          <PieChart
            :subtitle="offLine"
            :chartData="chartData"
            :selectedList="offlineSelectList"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { ref } from "vue";
import type { Ref } from "vue";
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
    console.log("chartData!!", props.chartData);

    const onLine = "Online";
    const offLine = "Offline";
    let onlinetotal: Ref<number> = ref(0);
    let onV: any;
    let onlineSelectList: Ref<string[]> = ref([]);

    const selectListsview = (selectLists: string[]) => {
      console.log("selectLists", selectLists);
      // selectLists가 바뀌면 value를 초기화 해야 함

      onlineSelectList.value = props.chartData.map((items: any) => {
        for (let i in selectLists) {
          if (items.countryCd == selectLists[i]) {
            onV =
              items.onlineErrorCount +
              items.onlineNormalCount +
              items.onlineWarningCount;

            console.log("it", onV);
          }
        }
        onlinetotal.value += onV;
        console.log("hhh", onlinetotal.value);
        return onlinetotal.value;
      });
    };

    // selectList데이터를 가공해서 piechart에 전달하기
    const offlineSelectList = props.chartData.map((items: object) => {
      return items;
    });

    return {
      onLine,
      offLine,
      selectListsview,
      onlineSelectList,
      offlineSelectList,
    };
  },
});
</script>

<style scoped lang="scss">
.container {
  margin-top: 40px;
  display: flex;
  justify-content: center;
}
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
    // background: yellow;
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
}
</style>
