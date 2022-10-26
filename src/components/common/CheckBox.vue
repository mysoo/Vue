<template>
  <div class="container">
    <div class="box">
      <input type="checkbox" value="all" v-model="allSelected" />
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

  <!-- <span>check: {{ selectList }}</span> -->
</template>

<script>
export default {
  name: "CheckBox",
  data() {
    return {
      checkList: [
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
      ],
      selectList: [],
    };
  },
  computed: {
    allSelected: {
      //getter
      get: function () {
        return this.checkList.length === this.selectList.length;
      },
      //setter
      set: function (e) {
        this.selectList = e ? this.checkList : [];
      },
    },
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
