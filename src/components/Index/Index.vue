<template>
  <div class="container" :style="{ height: height }">
    <div class="demo">
      <wxc-minibar
        title="weex"
        background-color="#009ff0"
        text-color="#FFFFFF"
        right-text="更多"
        @wxcMinibarLeftButtonClicked="minibarLeftButtonClick"
        @wxcMinibarRightButtonClicked="minibarRightButtonClick"
      ></wxc-minibar>
    </div>
    <div class="img-swiper">
      <div class="btn" @click="openLightBox">
        <text class="btn-txt">点击按钮弹出全屏图片</text>
      </div>
      <wxc-lightbox
        ref="wxc-lightbox"
        height="800"
        :show="show"
        :image-list="imageList"
        @wxcLightboxOverlayClicked="wxcLightboxOverlayClicked"
      ></wxc-lightbox>
    </div>
  </div>
</template>
<style>
.item-container {
  display: flex;
  width: 25%;
  background-color: #f2f3f4;
  align-items: center;
  justify-content: center;
}
.img-swiper{
  margin-top: 20px;
}
.btn-txt{
  height: 100px;
  line-height: 100px;
  width: 100%;
  padding: 50px;
  text-align: center;
  border:1px solid #ccc;
}
</style>

<script>
import { WxcMinibar, WxcTabBar,Utils,WxcLightbox } from "weex-ui";
const modal = weex.requireModule("modal");

export default {
  components: { 
   WxcLightbox, WxcMinibar
    },
     data: function () {
      return {
        imageList: [
          { src: 'https://gd2.alicdn.com/bao/uploaded/i2/T14H1LFwBcXXXXXXXX_!!0-item_pic.jpg' },
          { src: 'https://gd1.alicdn.com/bao/uploaded/i1/TB1PXJCJFXXXXciXFXXXXXXXXXX_!!0-item_pic.jpg' },
          { src: 'https://gd3.alicdn.com/bao/uploaded/i3/TB1x6hYLXXXXXazXVXXXXXXXXXX_!!0-item_pic.jpg' }
        ],
        show: false
      };
    },
  methods: {
    minibarLeftButtonClick() {},
    minibarRightButtonClick() {
      modal.toast({ message: "click rightButton!", duration: 1 });
    },
    openLightBox () {
        this.show = true;
      },
      wxcLightboxOverlayClicked () {
      // 无状态组件，需要在此次关闭
        this.show = false;
      }
  },
  created () {
      const tabPageHeight = Utils.env.getPageHeight();
      // 如果页面没有导航栏，可以用下面这个计算高度的方法
      // const tabPageHeight = env.deviceHeight / env.deviceWidth * 750;
      const { tabStyles } = this;
      this.contentStyle = { height: (tabPageHeight - tabStyles.height) + 'px' };
    },
     
};
</script>