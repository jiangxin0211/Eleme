<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab-wrapper">
      <tab :tabs="tabs"></tab>
    </div>
  </div>
</template>

<script>
import VHeader from './components/v-header/v-header'
import Seller from './components/seller/seller'
import Goods from './components/goods/goods'
import Ratings from './components/ratings/ratings'
import Tab from './components/tab/tab'
import { getSeller } from 'api'

export default {
  name: 'app',
  data () {
    return {
      seller: {}
    }
  },
  computed: {
    tabs () {
      return [
        {
          label: '商品',
          component: Goods,
          data: {
            seller: this.seller
          }
        },
        {
          label: '评价',
          component: Ratings,
          data: {
            seller: this.seller
          }
        },
        {
          label: '商家',
          component: Seller,
          data: {
            seller: this.seller
          }
        }
      ]
    }
  },
  components: {
    VHeader,
    Tab,
    Seller,
    Goods,
    Ratings
  },
  created () {
    this._getSeller()
  },
  methods: {
    _getSeller () {
      getSeller().then((seller) => {
        this.seller = seller.data
        console.log(this.seller)
      })
    }
  }
}
</script>
<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  .tab-wrapper
    position: fixed
    top: 136px
    bottom: 0
    left: 0
    right: 0
</style>
