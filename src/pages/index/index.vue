<template>
    <div class="index">
        <div class="bookname">凡人修仙之仙界篇</div>
        <div class="time">更新时间:{{time}}</div>
        <div class="title">最新章节:<span class="context">{{title}}</span></div>
        <div class="read" @click="read(title)">阅读</div>
    </div>
</template>

<script>

export default {
    onShareAppMessage: function () {
        
    },
    data(){
        return {
            title : '',
            time : ''
        }
    },
    methods : {
        qidian(){
            wx.showLoading({	
                title: '加载中···',	
            })

            this.$fly.request({
            method: 'get', // get 请求方式
            url: '/qd'
            }).then(res => {
                this.title = res.title
                this.time = res.time
                // 停止下拉动作
                wx.stopPullDownRefresh();
            }).catch(function (error) {	
                console.log(error);	
                wx.hideLoading();	
            });
        },
        read(title) {
            wx.navigateTo({
            url: "/pages/reader/main?title="+title
          });
        }
    },
    onPullDownRefresh () {	
      this.qidian()	
    },
    created () {
      this.qidian()
  }
}
</script>

<style scoped>
    .index {
        height: 100vh;
        width: 100vw;
        font-size: 16px;
        background-color: aliceblue;
        text-align: center;
        padding-top: 10vh;
    }
    .read {
        text-align: center;
        width: 45%;
        height: 100rpx;
        border-radius: 10rpx;
        line-height: 100rpx;
        background:chocolate;
        color: #fff;
        font-size: 32rpx;
        margin: 100rpx auto 0 auto;
    }
    .context {
        color: red;
        margin-left: 5px;
    }
    .bookname {
        font-size: 18px;
    }
    .time {
        margin-top: 5%;
    }
    .title {
        margin-top: 5%;
    }
     
</style>


