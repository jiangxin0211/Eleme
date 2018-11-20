<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <tab></tab>
  </div>
</template>

<script>
import VHeader from './components/v-header/v-header'
import Tab from './components/tab/tab'
import { getSeller } from 'api'

export default {
  name: 'app',
  data () {
    return {
      seller: {}
    }
  },
  components: {
    VHeader,
    Tab
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
</style>
