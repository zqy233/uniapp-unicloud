<template>
  <view class="home">
    <!-- <view class="top_nav">
      <u-tabs
        :list="navlist"
        :activeStyle="{
          color: '#333',
          fontWeight: 'bold',
          transform: 'scale(1.08)',
        }"
        :inactiveStyle="{
          color: '#888',
          transform: 'scale(1)',
        }"
      ></u-tabs>
    </view> -->
    <skeleton></skeleton>
    <view class="content"></view>
    <u-back-top
      :scroll-top="scrollTop"
      top="0"
      :customStyle="{
        backgroundColor: '#fff',
        border: '1rpx solid #0199FE',
      }"
    ></u-back-top>
  </view>
</template>

<script>
export default {
  onPageScroll(e) {
    this.scrollTop = e.scrollTop;
  },
  data() {
    return {
      scrollTop: 0,
      navlist: [{ name: "最新" }, { name: "热门" }],
    };
  },
  onLoad() {},
  methods: {},
};
</script>

<style lang="scss" scoped>
.home {
  height: 200vh;
  background-image: linear-gradient(#ee9d39, #fbd978);
}
</style>
