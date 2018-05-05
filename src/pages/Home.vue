<template>
  <wxc-tab-bar :tab-titles="tabIconFontTitles"
               :tab-styles="tabIconFontStyles"
               title-type="iconFont"
               duration="0"
               @wxcTabBarCurrentTabSelected="wxcTabBarCurrentTabSelected">
    <!-- 第一个页面内容-->
    <div class="item-container" :style="contentStyle">
      <Recommend/>
    </div>
    <!-- 第二个页面内容-->
    <div class="item-container" :style="contentStyle"><text>特别推荐</text></div>

    <!-- 第三个页面内容-->
    <div class="item-container" :style="contentStyle"><text>消息中心</text></div>

    <!-- 第四个页面内容-->
    <div class="item-container" :style="contentStyle"><text>我的主页</text></div>
  </wxc-tab-bar>
</template>

<style scoped>
  .item-container {
    width: 750px;
    background-color: #f2f3f4;
  }
</style>
<script>
import { WxcTabBar, Utils, WxcMinibar } from 'weex-ui'
import Recommend from './Recommend'
export default {
  components: { WxcTabBar, WxcMinibar, Recommend},
  data: () => ({

    tabIconFontTitles: [
      {
        title: '推荐',
        codePoint: '\ue658'
      },
      {
        title: '发现',
        codePoint: '\ue6ce'
      },
      {
        title: '消息',
        codePoint: '\ue639',
        badge: 5
      },
      {
        title: '我的',
        codePoint: '\ue633',
        dot: true
      }
    ],
    tabIconFontStyles: {
      bgColor: '#FFFFFF',
      titleColor: '#666666',
      activeTitleColor: 'red',
      activeBgColor: '#FFFFFF',
      isActiveTitleBold: true,
      width: 160,
      height: 120,
      fontSize: 24,
      textPaddingLeft: 10,
      textPaddingRight: 10,
      iconFontSize: 50,
      iconFontColor: '#333333',
      iconFontMarginBottom: 8,
      activeIconFontColor: 'red',
      iconFontUrl: '//at.alicdn.com/t/font_637484_dogt0puldviy66r.ttf'
    }
  }),
  created () {
    const tabPageHeight = Utils.env.getPageHeight()
    // 如果页面没有导航栏，可以用下面这个计算高度的方法
    // const tabPageHeight = env.deviceHeight / env.deviceWidth * 750;
    const { tabIconFontStyles } = this
    this.contentStyle = { height: (tabPageHeight - tabIconFontStyles.height) + 'px' }
  },
  methods: {
    wxcTabBarCurrentTabSelected (e) {
      const index = e.page
      // console.log(index);
    }
  }
}
</script>
