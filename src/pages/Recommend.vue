<template>
        <div>
            <div class="topNav">
                <text class="iconfont">&#xe638;</text>
                <text class="">推荐</text>
                <text class="iconfont">&#xe636;</text>
            </div>
            <scroller class="scroller" :style="pageStyle">
                <refresh class="refresh" @refresh="onrefresh" @pullingdown="onpullingdown" :display="refreshing ? 'show' : 'hide'">
                    <text class="indicator-text">刷新中...</text>
                    <loading-indicator class="indicator"></loading-indicator>
                </refresh>

                <div class="list">
                    <div class="listItem" v-for="(item,index) in lists" >
                        <image class="userAvatar" :src="item.imgsrc" resize="cover"></image>
                        <div class="userInfo">
                            <div class="leftUserInfo">
                                <div class="leftTopUserInfo">
                                    <text class="text userName" >{{item.name}}</text>
                                    <text class="text" >{{item.age}}岁</text>
                                </div>
                                <div class="leftDownUserInfo">
                                    <text class="text" >{{item.location}}</text>
                                    <text class="text" >{{item.distance}}</text>
                                </div>
                            </div>

                            <div class="rightUserInfo"  @click="clickLike(index)"  >
                                <text class="iconfont rightBotton" :style="{color:item.isClick?'#d4237a':'#ddd'}" >&#xe652;</text>
                            </div>
                        </div>

                    </div>
                </div>
                <loading class="loading" @loading="loadmore" :display="loadinging ? 'show' : 'hide'">
                    <text class="indicator-text">拼命加载中...</text>
                </loading>
            </scroller>
        </div>
</template>
<script>
import { Utils } from 'weex-ui'
var domModule = weex.requireModule('dom')
var modal = weex.requireModule('modal')
const LOADMORE_COUNT = 4
domModule.addRule('fontFace', {
  'fontFamily': 'iconfont',
  'src': "url('http:////at.alicdn.com/t/font_637484_dogt0puldviy66r.ttf')"
})
export default {
  props: {
    tabHeight: {
      type: Number// 数组
    }
  },
  data: function () {
    return {
      refreshing: false,
      refreshText: '↓   pull to refresh...',
      columnCount: 2,
      columnGap: '10',
      columnWidth: 'auto',
      contentOffset: '0',
      loadinging: false,
      showHeader: false,
      showScrollbar: false,
      scrollable: true,
      showStickyHeader: false,
      appearImage: null,
      disappearImage: null,
      stickyHeaderType: 'none',
      bottonStyle: { color: '#dddddd'},
      lists: [
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201611/103/st2.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false},
        {imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false}]
    }
  },

  created () {
    const tabPageHeight = Utils.env.getPageHeight()
    this.pageStyle = {height: tabPageHeight - (this.tabHeight + 80) + 'px'}
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
          this.lists.push({imgsrc: 'http://t2.hddhhn.com/uploads/tu/201608/280/st1.png', name: '小姐姐', location: '苏州', distance: '1km', age: 18, isClick: false})
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
      console.log('dy: ' + event.dy)
      console.log('pullingDistance: ' + event.pullingDistance)
      console.log('viewHeight: ' + event.viewHeight)
    },
    clickLike (e) {
      modal.toast({ message: '打招呼成功', duration: 0.5 })
      this.lists[e].isClick = true
    }

  }
}
</script>
<style>
    .iconfont{
        font-family: iconfont;
        font-size: 40px;
    }
    .scroller{
        width: 750px;
        flex-direction: row;
    }
    .listItem{
        width: 360px;
        height: 430px;
        margin-bottom: 10px;
        box-shadow: 1px 1px 2px #dddddd;
        background-color: white;
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
    .userAvatar{
        width: 360px;
        height: 350px;
    }
    .refresh {
      width: 750px;
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
    .loading {
        width: 750px;
        display: -ms-flex;
        display: -webkit-flex;
        display: flex;
        -ms-flex-align: center;
        -webkit-align-items: center;
        -webkit-box-align: center;
        align-items: center;
    }
    .indicator {
      height: 40px;
      width: 40px;
      color: blue;
    }
    .text{
        color: #717171;
        font-size: 25px;
        margin-right: 20px;
    }
    .leftTopUserInfo{
        flex-direction: row;
        align-items: center;
    }
    .leftDownUserInfo{
        flex-direction: row;
        font-size: 25px;
    }
    .list{
        width: 750px;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        height: auto;
        padding: 10px;
        justify-content: space-between;
    }
    .leftUserInfo{
        width: 100px;
        flex-direction: column;
        align-content: center;
        padding-left: 10px;
        flex: 1;
    }
    .userInfo{
        width: 360px;
        flex-direction: row;
    }
    .rightBotton{
        height: 80px;
        line-height: 80px;
        font-size: 70px;
        color: #dddddd;
    }
    .userName{
        font-size: 30px;
        color: #081107;
    }
</style>
