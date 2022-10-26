<template>
  <div class="container">
    <div class="box">
      <div><CheckBox /></div>
    </div>
  </div>
</template>

<script lang="ts">
import CheckBox from "../common/CheckBox.vue";

export default {
  name: "ChartMain",
  components: { CheckBox },
  data() {
    return {};
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
  min-height: 90px;
  width: 85%;
  box-shadow: 3px 3px 3px 3px #7aade0;
  border-radius: 10px;
}
</style>
