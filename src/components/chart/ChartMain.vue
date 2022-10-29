<template>
  <div class="container">
    <div class="box">
      <div><CheckBox /></div>
      <div><PieChart :chartData="chartData" /></div>
      <!-- <div>{{ name }}</div> -->
      <!-- checkbox value를 emit으로 piechart에 전달 -->
      <!-- emit실패,, store에 저장해서 넘기는걸로 수정해보자 -->
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
  },

  // setup(props: object) {
  //   console.log(props);
  //   return {};
  // },
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
}
</style>
