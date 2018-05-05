<template>
        <div>
            <div class="topNav">
                <text class="iconfont">&#xe638;</text>
                <text class="">推荐</text>
                <text class="iconfont">&#xe636;</text>
            </div>
            <list class="page" :style="pageStyle" @loadmore="loadmore" loadmoreoffset="10">
              <refresh class="refresh" @refresh="onrefresh" @pullingdown="onpullingdown" :display="refreshing ? 'show' : 'hide'">
                 <text class="indicator-text">上次刷新时间 2018-05-05 10:39</text>
                 <loading-indicator class="indicator"></loading-indicator>
               </refresh>
              <div class="list">
                  <div class="listItem"  v-for="item in lists">
                          <image style="width:360px;height:360px" :src="item.imgsrc"></image>
                          <div class="userInfo">
                              <text>{{item.name}}</text>

                          </div>

                  </div>
              </div>
           </list>
        </div>
</template>
<script>
var domModule = weex.requireModule('dom')
var modal = weex.requireModule('modal')
const LOADMORE_COUNT = 4
import { Utils } from 'weex-ui'
domModule.addRule('fontFace', {
  'fontFamily': 'iconfont',
  'src': "url('http:////at.alicdn.com/t/font_637484_dogt0puldviy66r.ttf')"
})
export default {
  props: {
      tabHeight: {
        type: Number//数组
      },
  },
  data: function () {

    return {
      refreshing: false,
      lists:[
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201611/103/st2.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'},
        {imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'}]

    }
  },

  created () {
    const tabPageHeight = Utils.env.getPageHeight()
    this.pageStyle={height:tabPageHeight-(this.tabHeight+80)+'px'}
  },

  methods: {
    loadmore: function (e) {
      modal.toast({
          message: 'This is a toast',
          duration: 0.3
      })
      setTimeout(() => {
          const length = this.lists.length
          for (let i = length; i < length + LOADMORE_COUNT; ++i) {
            this.lists.push({imgsrc:'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png',name:'小姐姐',location:'苏州',distance:'1km'})
          }
        }, 800)
    },
    onrefresh (event) {
      modal.toast({ message: 'Refreshing', duration: 1 })
      this.refreshing = true
      setTimeout(() => {
        this.refreshing = false
      }, 2000)
    },
    onpullingdown (event) {
      console.log("dy: " + event.dy)
      console.log("pullingDistance: " + event.pullingDistance)
      console.log("viewHeight: " + event.viewHeight)
    }
  }
}
</script>
<style>
    .iconfont{
        font-family: iconfont;
        font-size: 40px;
    }
    .page{
        width: 750px;
    }
    .userImage{
      width: 360px;
      height:300px;
    }
    .listItem{
        width: 360px;
        height: 450px;
        margin-left: 10px;
        margin-top: 5px;
        margin-bottom: 5px;
        box-sizing: border-box;
        border-top: 0.5px solid #ddd;
        border-left: 0.5px solid #ddd;
        border-bottom: 0.5px solid #ddd;
        border-right: 0.5px solid #ddd;
    }
    .list{
      width: 750px;
      flex-direction: row;
      flex-wrap: wrap;
    }
    .topNav{
        flex-direction: row;
        height:80px;
        justify-content: space-between;
        align-items: center;
        padding-left: 10px;
        padding-right: 10px;
        background-color: white;
        top: 0px;
        width: 750px;
    }
    .text {
        font-size: 88px;
        text-align: center;
        color: #41B883;
    }
    .refresh {
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
      font-size: 30px;
      text-align: center;
    }
    .indicator {
      margin-top: 16px;
      height: 40px;
      width: 40px;
      color: blue;
    }
    .userInfo{
      display: flex;
      height: 80px;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }
</style>
