<template>
  <div>
    <p class="title">{{title}}</p>
    <p class="art">{{art}}</p>
  </div>
</template>

<script>
import flyio from 'flyio'

export default {
  data () {
    return {
      art: '',
      title: ''
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

<style scoped>
  .art{
    font-size: 16px;
    background-color: ivory;
  }

</style>
