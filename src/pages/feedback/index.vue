<template>
  <div class="feedback">
    <div class="title">
      意见与反馈
    </div>
    <div class="cont">
      <textarea class="text" max='150' name="" v-model="content" placeholder="请填写你的意见和反馈"></textarea>
      <span>{{content.length}}/150</span>
    </div>
    <div @click="submitMes" class="bottom">
      提交
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        content: ''
      };
    },
    components: {},
    methods: {
      async submitMes() {
        this.$fly.request({
          method: 'post', // post 请求方式
          url: '/feedback/submitAction',
          body:{content: this.content}
        }).then(res => {
          this.art = res
        })
      },
    },
    computed: {}
  };
</script>
<style scoped>
  .feedback {
  height: 100%;
  background: #fff;
  padding: 0 20rpx;
  }
  .title {
    padding: 20rpx 0;
    border-bottom: 1rpx solid #d9d9d9;
  }
  .cont {
    position: relative;
    border-bottom: 1rpx solid #d9d9d9;
  }
    .text {
      height: 300rpx;
      padding: 20rpx;
    }
    span {
      position: absolute;
      right: 20rpx;
      bottom: 20rpx;
    }
  .connect {
    height: 100rpx;
    line-height: 100rpx;
    display: flex;
    border-bottom: 1rpx solid #d9d9d9;
  }
    label {
      width: 150rpx;
      height: 100%;
      display: inline-block;
    }
    input {
      flex: 1;
      display: inline-block;
      height: 100%;
    }
  .bottom {
    text-align: center;
    width: 95%;
    height: 100rpx;
    border-radius: 10rpx;
    line-height: 100rpx;
    background: #B4282D;
    color: #fff;
    font-size: 32rpx;
    margin: 100rpx auto 0 auto;
}
</style>