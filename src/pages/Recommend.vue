<template>

        <div>
            <div class="topNav">
                <text class="iconfont">&#xe638;</text>
                <text class="">推荐</text>
                <text class="iconfont">&#xe636;</text>
            </div>
            <waterfall class="page" ref="waterfall"
                       v-bind:style="{padding:padding}"
                       :column-width="columnWidth" :column-count="columnCount"
                       column-gap="0"
                       left-gap="0"
                       :show-scrollbar="showScrollbar" :scrollable="scrollable"
                       @scroll="recylerScroll" @loadmore="loadmore" loadmoreoffset=3000
            >
                <cell  v-for="num in items">
                        <div class="listItem">{{num.name}}</div>
                </cell>
            </waterfall>
        </div>

</template>
<script>
var domModule = weex.requireModule('dom')

domModule.addRule('fontFace', {
  'fontFamily': 'iconfont',
  'src': "url('http:////at.alicdn.com/t/font_637484_dogt0puldviy66r.ttf')"
})
export default {
  data: function () {
    const items = [
      {
        name: 'Thomas Carlyle',
        desc: 'Genius only means hard-working all one\'s life',
        behaviourName: 'Change width',
        behaviour: 'changeColumnWidth'
      },
      {
        desc: 'The man who has made up his mind to win will never say "impossible "',
        behaviourName: 'Change gap',
        behaviour: 'changeColumnGap'
      },
      {
        desc: 'There is no such thing as a great talent without great will - power',
        behaviourName: 'Change count',
        behaviour: 'changeColumnCount'
      },
      {
        name: 'Addison',
        desc: 'Cease to struggle and you cease to live',
        behaviourName: 'Show scrollbar',
        behaviour: 'showScrollbar'
      },
      {
        desc: 'A strong man will struggle with the storms of fate',
        behaviourName: 'Listen appear',
        behaviour: 'listenAppear'
      },
      {
        name: 'Ruskin',
        desc: 'Living without an aim is like sailing without a compass',
        behaviourName: 'Set scrollable',
        behaviour: 'setScrollable'
      },
      {
        behaviourName: 'waterfall padding',
        behaviour: 'setPadding'
      },
      {
        name: 'Balzac',
        desc: 'There is no such thing as a great talent without great will - power',
        behaviourName: 'listen scroll',
        behaviour: 'listenScroll'
      }
    ]

    let repeatItems = []
    for (let i = 0; i < 3; i++) {
      repeatItems.push(...items)
    }

    return {
      padding: 0,
      refreshing: false,
      refreshText: '↓   pull to refresh...',
      columnCount: 2,
      columnGap: 0,
      columnWidth: 'auto',
      contentOffset: '0',
      showHeader: true,
      showScrollbar: false,
      scrollable: true,
      showStickyHeader: false,
      appearImage: null,
      disappearImage: null,
      stickyHeaderType: 'none',
      // fixedRect:'',
      items: repeatItems
    }
  },

  created () {
    // let self = this
    // setTimeout(()=>{
    //   weex.requireModule('dom').getComponentRect(this.$refs.fixed, result=>{
    //     const x = result.size.left
    //     const y = result.size.top
    //     const width = result.size.width
    //     const height = result.size.height
    //     self.fixedRect = `${x}|${y}|${width}|${height}`
    //   })
    // }, 3000)
  },

  methods: {
    recylerScroll: function (e) {
      this.contentOffset = e.contentOffset.y
    },
    loadmore: function (e) {
      console.log('receive loadmore event')
      // this.$refs.waterfall.resetLoadmore()
    },
    showOrRemoveHeader: function () {
      this.showHeader = !this.showHeader
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
        height: 1000px;
        padding-left: 7.5px;
    }
    .listItem{
        width: 365px;
        height: 300px;
        background-color: #00B4FF;
        margin-top: 6px;

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
</style>
