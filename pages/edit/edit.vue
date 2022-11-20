<template>
  <view class="edit">
    <view class="title">
      <input
        type="text"
        placeholder="请输入标题"
        placeholder-class="plactholderClass"
      />
    </view>
    <view class="content">
      <editor placeholder="请输入内容"></editor>
    </view>
    <view class="btn">
      <u-button type="primary" text="确认发表"></u-button>
    </view>
    <view class="tools">
      <view class="item">
        <text class="iconfont icon-zitibiaoti"></text>
      </view>
      <view class="item">
        <text class="iconfont icon-bold"></text>
      </view>
      <view class="item">
        <text class="iconfont icon-minus-bold"></text>
      </view>
      <view class="item">
        <text class="iconfont icon-icon"></text>
      </view>
      <view class="item">
        <text class="iconfont icon-qingxie-"></text>
      </view>
      <view class="item">
        <text class="iconfont icon-select-bold"></text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.edit {
  padding: 30rpx;
  .title {
    input {
      margin-bottom: 30rpx;
      height: 120rpx;
      font-size: 36rpx;
      border-bottom: 1px solid #e4e4e4;
    }
    .plactholderClass {
      font-style: normal;
      color: #e0e0e0;
      font-family: Georgia, "Times New Roman", Times, serif;
    }
  }
  /deep/ .ql-blank::before {
    font-style: normal;
    color: #e0e0e0;
    font-family: Georgia, "Times New Roman", Times, serif;
  }
  .content {
    height: calc(100vh - 500rpx);
    margin-bottom: 30rpx;
  }
  .tools {
    width: 100%;
    height: 80rpx;
    position: fixed;
    left: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-top: 1rpx solid #f4f4f4;
    .item {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .iconfont {
      font-size: 36rpx;
      color: #333;
      &.active {
        color: #0199fe;
      }
    }
  }
}
</style>
