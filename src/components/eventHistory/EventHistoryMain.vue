<template>
  <div class="listbox">
    <div>
      <ItemCard :title="title" :eventHistoryDatas="eventHistoryDatas" />
    </div>
  </div>
</template>

<script lang="ts">
import ItemCard from "../common/ItemCard.vue";
export default {
  name: "EventHistoyMain",
  components: { ItemCard },
  props: {
    eventHistoryDatas: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },
  setup() {
    const title = "Event History";
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
