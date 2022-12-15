<template>
  <view class="edit">
    <view class="title">
      <input
        type="text"
        placeholder="请输入标题"
        placeholder-class="plactholderClass"
        v-model="artObj.title"
      />
    </view>
    <editor
      class="content"
      id="editor"
      placeholder="请输入内容"
      @ready="onEditorReady"
      @input="onEditorInput"
      @statuschange="statuschange"
    ></editor>
    <view class="btn">
      <u-button
        type="primary"
        text="确认发表"
        :disabled="!artObj.title.length"
      ></u-button>
    </view>
    <view class="tools">
      <view class="item" @click="clickHeader">
        <text
          class="iconfont icon-zitibiaoti"
          :class="headerShow ? 'active' : ''"
        ></text>
      </view>
      <view class="item" @click="clickBold">
        <text
          class="iconfont icon-bold"
          :class="boldShow ? 'active' : ''"
        ></text>
      </view>
      <view class="item" @click="addDivider">
        <text class="iconfont icon-minus-bold"></text>
      </view>
      <view class="item" @click="addImg">
        <text class="iconfont icon-icon"></text>
      </view>
      <view class="item" @click="clickItailc">
        <text
          class="iconfont icon-qingxie-"
          :class="boldShow ? 'active' : ''"
        ></text>
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
    return {
      headerShow: false,
      boldShow: false,
      itailcShow: false,
      artObj: {
        title: "",
        content: "",
        description: ""
      }
    }
  },
  methods: {
    /** 初始化编辑器 */
    onEditorReady() {
      // #ifdef APP-PLUS || H5 ||MP-WEIXIN
      uni
        .createSelectorQuery()
        .in(this)
        .select("#editor")
        .context(res => {
          this.editorCtx = res.context
        })
        .exec()
      // #endif
    },
    /** 编辑器样式改变 */
    statuschange(e) {
      console.log(e)
      const { detail } = e
      this.headerShow = detail.hasOwnProperty("header")
      this.boldShow = detail.hasOwnProperty("bold")
      this.itailcShow = detail.hasOwnProperty("itailc")
      // this.editorCtx.scrollIntoView()
    },
    /** 编辑器输入 */
    onEditorInput(e) {
      console.log(e)
    },
    /** 添加标题 */
    clickHeader() {
      this.headerShow = !this.headerShow
      this.editorCtx.format("header", this.headerShow ? "H2" : false)
      // setTimeout(() => {
      // }, 150)
    },
    /** 文字加粗 */
    clickBold() {
      this.boldShow = !this.boldShow
      this.editorCtx.format("bold", this.boldShow)
      this.editorCtx.scrollIntoView()
    },
    /** 添加图片 */
    addImg() {
      uni.chooseImage({
        success: async res => {
          console.log(res)
          uni.showLoading({
            title: "图片上传中",
            mask: true
          })
          for (let item of res.tempFiles) {
            let res = await uniCloud.uploadFile({
              filePath: item.path,
              cloudPath: item.name
            })
            this.editorCtx.insertImage({ src: res.fileID })
          }
          uni.hideLoading()
        }
      })
    },
    /** 文字倾斜 */
    clickItailc() {
      this.headerShow = !this.headerShow
      this.editorCtx.format("italic")
    },
    /** 添加分割线 */
    addDivider() {
      this.editorCtx.insertDivider()
    }
  }
}
</script>

<style lang="scss" scoped>
.edit {
  height: 100%;
  padding: 30rpx 30rpx 80rpx 30rpx;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  .title {
    margin-bottom: 30rpx;
    input {
      height: 80rpx;
      font-size: 36rpx;
      border-bottom: 1px solid #e4e4e4;
    }
    .plactholderClass {
      font-style: normal;
      color: #e0e0e0;
      font-family: Georgia, "Times New Roman", Times, serif;
    }
  }
  /deep/ .ql-editor.ql-blank::before {
    font-style: normal;
    color: #e0e0e0;
    font-family: Georgia, "Times New Roman", Times, serif;
  }
  .content {
    flex-grow: 1;
    margin-bottom: 10px;
  }
  .btn {
    margin-bottom: 10px;
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
    border-top: 1rpx solid #cdcdcd;
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
