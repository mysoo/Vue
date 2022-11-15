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
  &.listbox {
    box-sizing: border-box;
    display: flex;
  }
}
</style>
