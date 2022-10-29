<template>
  <div>
    <div class="container">
      <div class="box">
        <input type="checkbox" value="all" v-model="allselected" />
        <label for="all">All</label>

        <div class="cb" v-for="(item, index) in checkList" :key="index">
          <input
            type="checkbox"
            :id="item"
            :value="item"
            v-model="selectList"
            :key="index"
          />
          <label :for="item" :key="index + '1'"> {{ item }}</label>
        </div>
      </div>
    </div>

    <div>
      <span>check: {{ selectList }}</span>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "CheckBox",
  setup() {
    const checkList: string[] = [
      "Republic of Korea",
      "Germany",
      "United Kingdom",
      "Italy",
      "Portugal",
      "France",
      "Austria",
      "Denmark",
      "Morocco",
      "Australia",
      "etc",
    ];
    const selectList: string[] = [];
    const allselected = (): string[] => {
      console.log(checkList);
      checkList.map((i) => selectList.push(i));
      return selectList;
    };

    return {
      checkList,
      selectList,
      allselected,
    };
  },
};
</script>

<style scoped lang="scss">
.container {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
}
.box {
  box-sizing: border-box;
  display: inline;
  justify-content: center;
  width: 90%;
  font-size: 1em;
  background-color: rgb(223, 217, 217);
  padding: 2.5%;
  border-radius: 10px;
}
.cb {
  box-sizing: border-box;
  display: inline;
  text-align: center;
  padding-left: 2.2%;
}
</style>
