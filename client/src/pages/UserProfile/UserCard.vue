<template>
  <md-card class="md-card-profile">
    <div class="md-card-avatar">
      <img class="img" :src="cardUserImage" />
    </div>

    <md-card-content>
      <h6 class="category text-gray">CEO / Co-Founder</h6>
      <h4 class="card-title">Alec Thompson</h4>
      <p class="card-description">
        Nguyên tắc quản lý dự án:
        Trách nhiệm
        Tôn trọng
        Công bằng và
        Trung thực
      </p>
      <md-button class="md-round md-success">Tìm hiểu thêm</md-button>
    </md-card-content>
  </md-card>
</template>
<script>
export default {
  name: "user-card",
  props: {
    cardUserImage: {
      type: String,
      default: require("@/assets/img/faces/marc.jpg"),
    },
  },
  data() {
    return {};
  },
};
</script>
<style></style>
