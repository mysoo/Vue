<template>
  <p v-if="serialNO">
    <span>{{ title }}</span>
    <span class="iv">{{ value }}</span>
  </p>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "InputForm",
  props: {
    title: String,
    value: String,
  },
  setup() {
    return {};
  },
});
</script>

<style scoped lang="scss">
span {
  padding-right: 50px;
  display: flex;
  min-width: 30%;
}
p {
  display: flex;
  flex-direction: row;
}
.iv {
  display: flex;
  min-width: 50%;
  font-weight: bold;
}
</style>
