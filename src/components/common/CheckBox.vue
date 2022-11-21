<template>
  <div>
    <div class="container">
      <div class="box">
        <input
          type="checkbox"
          value="all"
          v-model="allselected"
          @click="allCheck"
          @change="deliverSelectList"
        />
        <label for="all">All</label>

        <div class="cb" v-for="(item, index) in checkList" :key="index">
          <input
            @change="deliverSelectList"
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
    <!-- 
    <div>
      <span>check: {{ selectList }}</span>
    </div> -->
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";
import type { Ref } from "vue";

export default defineComponent({
  name: "CheckBox",
  props: {},

  setup(props, context) {
    const { emit } = context;
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
    for (let i = 0; i < checkList.length; i++) {
      selectList.value.push(String(checkList[i]));
    }
    let allselected = ref(true);
    const allCheck = () => {
      if (!allselected.value) {
        if (selectList.value.length != 0) {
          selectList.value = [];
        }
        for (let i = 0; i < checkList.length; i++) {
          selectList.value.push(String(checkList[i]));
        }
        allselected.value = true;
      } else {
        selectList.value = [];
        allselected.value = false;
      }
    };
    const deliverSelectList = computed(() => {
      return emit("selectList", selectList.value);
    });

    return {
      checkList,
      selectList,
      allselected,
      allCheck,
      deliverSelectList,
    };
  },
});
</script>

<style scoped lang="scss">
.container {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  .box {
    box-sizing: border-box;
    display: inline;
    width: 90%;
    font-size: 1em;
    background-color: rgb(223, 217, 217);
    padding: 2.5%;
    border-radius: 10px;
  }
}
.cb {
  box-sizing: border-box;
  display: inline;
  text-align: center;
  padding-left: 2.2%;
}
</style>
