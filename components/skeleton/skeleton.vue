<template>
  <view class="loading">
    <u-skeleton
      rows="5"
      title
      loading
      :rowsHeight="['18px', '18px', '80px']"
      class="gap"
    ></u-skeleton>
    <u-skeleton
      rows="5"
      :title="false"
      loading
      :rowsHeight="['18px', '18px', '80px']"
    ></u-skeleton>
  </view>
</template>

<script>
export default {
  name: "skeleton",
  data() {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.loading {
  padding: 30rpx;
  .gap {
    margin-bottom: 10px;
  }
}
</style>
