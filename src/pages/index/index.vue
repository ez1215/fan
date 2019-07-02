<template>
    <div class="index">
        <div>凡人修仙之仙界篇</div>
        <div class="time">更新时间:{{time}}</div>
        <div class="title">最新章节:{{title}}</div>
        <div @click="read">阅读</div>
    </div>
</template>

<script>
export default {
    data(){
        return {
        title : '',
        time : ''
        }
    },
    methods : {
        qidian(){
            this.$fly.request({
            method: 'get', // get 请求方式
            url: '/qd'
            }).then(res => {
                this.title = res.title
                this.time = res.time
            })
        },
        read() {
            wx.navigateTo({
            url: "/pages/reader/main"
          });
        }
    },
    created () {
      this.qidian()
  }
}
</script>

<style scoped>
    .index {
        font-size: 14px;
        background-color: aliceblue
    }
/* 
    .time {
        
    }
    .title {
        font-size: 14px;
    }
     */
</style>


