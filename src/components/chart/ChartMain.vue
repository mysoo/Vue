<template>
  <div class="container">
    <div class="box">
      <div><CheckBox @selectList="selectList" /></div>
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
            :selectedList="selectList"
          />
        </div>

        <div>
          <PieChart
            :subtitle="offLine"
            :chartData="chartData"
            :selectedList="selectList"
          />
        </div>
      </div>

      <!-- checkbox value를 emit으로 piechart에 전달 -->
    </div>
  </div>
</template>

<script lang="ts">
import CheckBox from "../common/CheckBox.vue";
import PieChart from "../chart/PieChart.vue";

export default {
  name: "ChartMain",
  components: { CheckBox, PieChart },
  props: {
    chartData: {
      type: Object,
      default: () => {
        return {};
      },
    },
    selectList: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },

  setup() {
    const onLine = "Online";
    const offLine = "Offline";
    return { onLine, offLine };
  },
};
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
