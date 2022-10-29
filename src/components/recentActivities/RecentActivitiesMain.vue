<template>
  <div class="listbox">
    <div>
      <ItemCard :title="title" :RecentActivitiesDatas="RecentActivitiesDatas" />
    </div>
  </div>
</template>

<script lang="ts">
import ItemCard from "../common/ItemCard.vue";
export default {
  name: "RecentActivitiesMain",
  components: { ItemCard },
  props: {
    RecentActivitiesDatas: {
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
};
</script>

<style scoped lang="scss">
.container {
  margin-top: 40px;
  display: flex;
  width: 100%;
  justify-content: center;
  flex-direction: column;
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
.listbox {
  box-sizing: border-box;
  display: flex;
}
</style>
