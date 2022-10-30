<template>
  <div>
    <div class="container">
      <div class="box">
        <input type="checkbox" :value="all" v-model="allselected" />
        <label for="all">All</label>

        <div class="cb" v-for="(item, index) in checkList" :key="index">
          <input
            @input="() => $emit('selectList', selectList)"
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
import { ref } from "vue";
import type { Ref } from "vue";
export default {
  name: "CheckBox",
  props: {
    all: {
      type: Boolean,
      default: true,
    },
  },
  model: {
    props: "all",
    event: "input",
  },

  setup() {
    // const allselected = true;
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
    let selectList: Ref<string[]> = ref([]);
    const allselected = ref(true);

    // const allselected = selectList.value;

    // const allselected = (): string[] => {
    //   // console.log(checkList);
    //   // selectList.value.push(checkList);
    //   checkList.map((i) => selectList.value.push(i));
    //   // checkList.map((i) => (selectList.value = sel));
    //   console.log("g", selectList.value);
    //   return selectList.value;
    // };

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
