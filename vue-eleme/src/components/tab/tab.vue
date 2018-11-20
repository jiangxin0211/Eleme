<template>
  <div class="tab">
    <cube-tab-bar
      :showSlider=true
      :useTransition=false
      v-model="selectedLabel"
      :data="tabs"
      ref="tabBar"
      class="boder-bottom-1px"
    ></cube-tab-bar>
    <div class="slide-wrapper">
      <cube-slide
        :loop=false
        :auto-play=false
        :show-dots=false
        :initial-index="index"
        ref="slide"
        @change="onChange"
        @scroll="onScorll"
        :options="slideOptions"
      >
        <cube-slide-item v-for="(tab, index) in tabs" :key="index">
          <component :is="tab.component" :data="tab.data"></component>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script>
export default {
  name: "tab",
  props: {
    tabs: {
      type: Array,
      default () {
        return {}
      }
    },
    initialIndex: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      index: this.initialIndex,
      slideOptions: {
        listenScroll: true,
        probeType: 3,
        directionLockThreshold: 0
      }
    }
  },
  computed: {
    selectedLabel: {
      // v-model  双向数据绑定  当我们点击tabBar时，会去修改selectedLabel；所以要设置一个setter，
      // setter时为了计算当前的index，index的改变，实现slide的切换
      get () {
        return this.tabs[this.index].label
      },
      set (newVal) {
        this.index = this.tabs.findIndex((value) => {
          return value.label === newVal
        })
      }
    }
  },
  methods: {
    onChange (current) {
      this.index = current
    },
    onScorll (pos) {
      const tabBarWidth = this.$refs.tabBar.$el.clientWidth
      const slideWidth = this.$refs.slide.slide.scrollerWidth
      const transform = -pos.x / slideWidth * tabBarWidth
      this.$refs.tabBar.setSliderTransform(transform)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import "~common/stylus/mixin.styl"
  .tab
    >>> .cube-tab
          padding: 10px 0
    display: flex
    flex-direction: column
    height: 100%
    .slide-wrapper
      flex: 1
      text-align: center
      overflow: hidden
</style>
