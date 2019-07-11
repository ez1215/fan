<template>
  <div class="body">
    <div class="main">
      <p class="art">{{art}}</p>
    </div>
  </div>
</template>

<style scoped>
  .art{
    font-size: 35rpx;
    background-color: ivory;
    
  }

  .main {
    height: 100%;
    width: 100%;
  }

  .body {
    height: 100%;
    width: 100%;
  }

</style>

<script>
import flyio from 'flyio'

export default {
  data () {
    return {
      art: ''
    }
  },

  methods: {
    load() {
         this.$fly.request({
          method: 'get', // get 请求方式
          url: '/getLeast'
        }).then(res => {
          this.art = res
        })
    }
  },
  onLoad: function(options) {
    wx.setNavigationBarTitle({
        title: options.title
      })
  },
  created () {
      this.load()
  }
}
</script>
