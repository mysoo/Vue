<template>
  <div class="home">
    <ChartMain :chartData="datas" />
    <div class="container">
      <div class="lists">
        <EventHistoryMain :eventHistoryDatas="eventHistoryDatas" />
        <RecentActivitiesMain :RecentActivitiesDatas="RecentActivitiesDatas" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import jsonData from "../components/json/data.json";
import ChartMain from "../components/chart/ChartMain.vue";
import EventHistoryMain from "../components/eventHistory/EventHistoryMain.vue";
import RecentActivitiesMain from "../components/recentActivities/RecentActivitiesMain.vue";
export default defineComponent({
  name: "HomeView",
  components: {
    ChartMain,
    EventHistoryMain,
    RecentActivitiesMain,
  },

  setup() {
    const datas = jsonData.chart.map((items: object) => {
      return items;
    });
    const eventHistoryDatas = jsonData.event.map((items: object) => {
      return items;
    });
    const RecentActivitiesDatas = jsonData.activity.map((items: object) => {
      return items;
    });
    return {
      datas,
      eventHistoryDatas,
      RecentActivitiesDatas,
    };
  },
});
</script>

<style scoped lang="scss">
.container {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
}
.lists {
  box-sizing: border-box;
  width: 85%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
