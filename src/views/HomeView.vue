<template>
  <div class="home">
    <ChartMain :chartData="datas" />
    <!-- <h1 v-for="(item, index) in datas" :key="index">{{ item }}</h1> -->
    <!-- emit으로 값 가져오기 -->

    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ChartMain from "../components/chart/ChartMain.vue";
import jsonData from "../components/json/data.json";

export default defineComponent({
  name: "HomeView",
  components: {
    // HelloWorld,
    // data,
    ChartMain,
  },

  methods: {},
  computed: {
    datas() {
      return jsonData.chart.map((items) => {
        return items;
      });
    },
  },
});
</script>
