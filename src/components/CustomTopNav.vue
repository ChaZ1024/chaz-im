<template>
    <div class="topNav">
        <text class="iconfont">{{leftIconCode}}</text>
        <text class="">{{titleText}}</text>
        <text class="iconfont">{{rightIconCode}}</text>
    </div>
</template>
<script>
var domModule = weex.requireModule('dom')

domModule.addRule('fontFace', {
  'fontFamily': 'iconfont',
  'src': "url('http:////at.alicdn.com/t/font_637484_dogt0puldviy66r.ttf')"
})
export default {
  props: {
    titleText: {
      type: String// 数组
    },
    leftIconCode: {// 字符串
      type: String
    },
    rightIconCode: {// 字符串
      type: String
    }
  },
  methods: {
  }
}
</script>

<style>
    .iconfont{
        font-family: iconfont;
        font-size: 40px;
    }
    .topNav{
        flex-direction: row;
        height:80px;
        justify-content: space-between;
        align-items: center;
        padding-left: 10px;
        padding-right: 10px;
        background-color: white;
        position: fixed;
        top: 0px;
        width: 100%;

    }
</style>
