<template>
  <div class="container">
    <div class="title">
      <p>{{ title }}</p>
      <button class="btn">
        <img class="img" alt="arrow img" src="../../assets/right-arrow.png" />
      </button>
    </div>
    <div>
      <ItemList
        :eventHistoryDatas="eventHistoryDatas"
        v-for="(event, index) in eventHistoryDatas"
        :key="index"
        :serialNO="event.deviceId"
        :event="event.eventCategory"
        :category="null"
        :startDate="event.createDt"
        :eventCode="event.eventCode"
        :newFlag="event.newFlag"
      />
    </div>

    <div>
      <ItemList
        :RecentActivitiesDatas="RecentActivitiesDatas"
        v-for="(activity, index) in RecentActivitiesDatas"
        :key="index"
        :serialNO="activity.deviceId"
        :date="activity.createDt"
        :activityType="activity.activityType"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ItemList from "./ItemList.vue";

export default defineComponent({
  name: "ItemCard",
  components: {
    ItemList,
  },
  props: {
    title: String,
    eventHistoryDatas: {
      type: Object,
      default: () => {
        return {};
      },
    },
    RecentActivitiesDatas: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },
  setup() {
    return;
  },
});
</script>

<style scoped lang="scss">
.container {
  box-sizing: border-box;
  box-shadow: 3px 3px 3px 3px #7aade0;
  border-radius: 10px;
  margin-top: 30px;
  padding-bottom: 30px;
  display: flex;
}
.title {
  box-sizing: border-box;
  border-radius: 10px 10px 0 0;
  width: 100%;
  background-color: #658db4;
  font-weight: bold;
  font-size: 1.5em;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: black;
  p {
    padding-left: 55px;
  }
  .img {
    height: 20px;
    width: 20px;
    padding-right: 55px;
  }
  .btn {
    background: none;
    border: none;
    cursor: pointer;
  }
}
.content {
  p {
    display: flex;
    flex-direction: start;
    padding-left: 50px;
  }
}
</style>
