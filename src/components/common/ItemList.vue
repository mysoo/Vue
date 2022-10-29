<template>
  <div class="content">
    <p v-if="serialNO">
      <span>Serial No.</span>
      <span class="iv">{{ serialNO }}</span>
    </p>
    <p v-if="event">
      <span>Event</span>
      <span class="iv">{{ event }}</span>
    </p>
    <p v-if="event">
      <span>Category</span>
      <span class="iv">{{ category }}</span>
    </p>
    <p v-if="startDate">
      <span>Start Date</span>
      <span class="iv">{{ convertStartDate }}</span>
    </p>
    <p v-if="eventCode">
      <span>Event Code</span>
      <span class="iv">{{ eventCode }}</span>
    </p>
    <p v-if="newFlag">
      <span>new</span>
      <span class="iv">{{ newFlag }}</span>
    </p>
    <p v-if="date">
      <span>Date</span>
      <span class="iv">{{ convertDate }}</span>
    </p>
    <p v-if="activityType">
      <span>activityType</span>
      <span class="iv">{{ activityType }}</span>
    </p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import moment from "moment";

export default defineComponent({
  name: "ItemList",
  props: {
    title: String,
    serialNO: String,
    event: String,
    category: String,
    startDate: Number,
    eventCode: String,
    newFlag: String,
    date: Number,
    activityType: String,
  },
  setup(props) {
    const convertStartDate = moment(props.startDate).format("DD/MM/YYYY hh:mm");
    const convertDate = moment(props.date).format("DD/MM/YYYY hh:mm");

    return { convertStartDate, convertDate };
  },
});
</script>

<style scoped lang="scss">
.content {
  padding: 30px 300px 0px 50px;

  p {
    display: flex;
    flex-direction: row;
  }
  span {
    padding-right: 50px;
    display: flex;
    min-width: 30%;
  }
  .iv {
    display: flex;
    min-width: 50%;
    font-weight: bold;
  }
}
</style>
