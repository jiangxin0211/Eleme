<template>
  <div class="tab">
    <cube-tab-bar
      :showSlider=true
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
      >
        <cube-slide-item>
          <goods></goods>
        </cube-slide-item>
        <cube-slide-item>
          <ratings></ratings>
        </cube-slide-item>
        <cube-slide-item>
          <seller></seller>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script>
import Seller from '../../components/seller/seller'
import Goods from '../../components/goods/goods'
import Ratings from '../../components/ratings/ratings'
export default {
  name: "tab",
  data () {
    return {
      index: 0,
      tabs: [{
        label: '商品'
      }, {
        label: '评价'
      }, {
        label: '商家'
      }]
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
  components: {
    Seller,
    Goods,
    Ratings
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
