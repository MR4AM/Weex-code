<template>
    <div class="index">
       <text class="message">Now, let's use Vue.js to build your Weex app.</text>
        <slider class="slider" interval="3000" auto-play="true">
          <div class="frame" v-for="img in imageList">
            <image class="image" resize="cover" :src="img.src"></image>
          </div>
        </slider>
        <div class="wrapper">
          <div class="group">
            <text class="label">Time: </text>
            <text class="title">{{value}}</text>
          </div>
          <div class="group">
            <text class="button" @click="pickTime">Pick Time</text>
          </div>
        </div>
         <scroller class="scroller">
          <div class="cell" v-for="num in lists">
            <div class="panel">
              <text class="text">{{num}}</text>
              </div>
            </div>
            <loading class="loading" @loading="onloading" :display="loadinging ? 'show' : 'hide'">
              <text class="indicator-text">Loading ...</text>
              <loading-indicator class="indicator"></loading-indicator>
            </loading>
        </scroller>
  </div>
</template>
<style scoped>
  .index{
    overflow: auto;
  }
  .image {
    width: 700px;
    height: 700px;
  }
  .slider {
    margin-top: 25px;
    margin-left: 25px;
    width: 700px;
    height: 700px;
    border-width: 2px;
    border-style: solid;
    border-color: #41B883;
  }
  .frame {
    width: 700px;
    height: 700px;
    position: relative;
  }
  .wrapper {
    flex-direction: column;
    justify-content: center;
  }
  .group {
    flex-direction: row;
    justify-content: center;
    margin-bottom: 40px;
    align-items: center;
  }
  .label {
    font-size: 40px;
    color: #888888;
  }
  .title {
    font-size: 80px;
    color: #41B883;
  }
  .button {
    font-size: 36px;
    width: 280px;
    color: #41B883;
    text-align: center;
    padding-top: 25px;
    padding-bottom: 25px;
    border-width: 2px;
    border-style: solid;
    border-color: rgb(162, 217, 192);
    background-color: rgba(162, 217, 192, 0.2);
  }
  .loading {
    width: 750;
    display: -ms-flex;
    display: -webkit-flex;
    display: flex;
    -ms-flex-align: center;
    -webkit-align-items: center;
    -webkit-box-align: center;
    align-items: center;
  }
  .indicator-text {
    color: #888888;
    font-size: 42px;
    text-align: center;
  }
  .indicator {
    margin-top: 16px;
    height: 40px;
    width: 40px;
    color: blue;
  }
  .panel {
    width: 600px;
    height: 250px;
    margin-left: 75px;
    margin-top: 35px;
    margin-bottom: 35px;
    flex-direction: column;
    justify-content: center;
    border-width: 2px;
    border-style: solid;
    border-color: #DDDDDD;
    background-color: #F5F5F5;
  }
  .text {
    font-size: 50px;
    text-align: center;
    color: #41B883;
  }
</style>

<script>
const picker = weex.requireModule('picker')
  export default {
    data () {
      return {
        imageList: [
          { src: 'https://gd2.alicdn.com/bao/uploaded/i2/T14H1LFwBcXXXXXXXX_!!0-item_pic.jpg'},
          { src: 'https://gd1.alicdn.com/bao/uploaded/i1/TB1PXJCJFXXXXciXFXXXXXXXXXX_!!0-item_pic.jpg'},
          { src: 'https://gd3.alicdn.com/bao/uploaded/i3/TB1x6hYLXXXXXazXVXXXXXXXXXX_!!0-item_pic.jpg'}
        ],
        value:'',
        loadinging: false,
        lists: ['模块一', '模块二', '模块三', '模块四', '模块五']
      }
    },
    methods: {
      pickTime () {
        console.log(8888);
        //pickTime挑选时间，pickDate挑选日期
        picker.pickDate({
          value: this.value
        }, event => {
          if (event.result === 'success') {
            this.value = event.data
          }
        })
      },
      onloading (event) {
        modal.toast({ message: '正在为您加载，请稍等片刻', duration: 1 })
        this.loadinging = true
        setTimeout(() => {
          this.loadinging = false
        }, 2000)
      },
    }
  }
</script>
