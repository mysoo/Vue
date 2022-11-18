<template>
  <div class="container">
    <div class="listbox">
      <div>
        <div>
          <div class="title">
            <p>{{ title }}</p>
            <button class="btn">
              <img
                class="img"
                alt="arrow img"
                src="../../assets/right-arrow.png"
              />
            </button>
          </div>
          <div>
            <ItemList
              :recentActivitiesDatas="recentActivitiesDatas"
              v-for="(activity, index) in recentActivitiesDatas"
              :key="index"
              :serialNO="activity.deviceId"
              :date="activity.createDt"
              :activityType="activity.activityType"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- <div class="listbox">
    <div>
      <ItemCard :title="title" :recentActivitiesDatas="recentActivitiesDatas" />
    </div>
  </div> -->
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ItemList from "../common/ItemList.vue";
export default defineComponent({
  name: "RecentActivitiesMain",
  components: { ItemList },
  props: {
    recentActivitiesDatas: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },
  setup() {
    const title = "Recent Activities";
    return { title };
  },
});
</script>

<style scoped lang="scss">
.container {
  box-sizing: border-box;
  display: flex;
  height: auto;
  border-radius: 10px;
  margin-top: 40px;
  box-shadow: 3px 3px 3px 3px #7aade0;
  justify-content: center;
  flex-direction: column;
  &.listbox {
    box-sizing: border-box;
    display: flex;
  }
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
