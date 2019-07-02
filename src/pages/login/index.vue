<template>
  <div class="login">
    <div class="logo">
    </div>
    <button class="login-btn" open-type="getUserInfo" lang="zh_CN" @getuserinfo="doLogin">微信登录</button>
  </div>
</template>

<script>
  import {
    host
  } from "../../utils";
  var qcloud = require("wafer2-client-sdk/index.js");
  export default {
    created() {},
    mounted() {
      console.log(host);
      qcloud.setLoginUrl(host + "/login");
    },
    data() {
      return {};
    },
    components: {},
    methods: {
      doLogin() {
        wx.showLoading({
          title: "登录中...", //提示的内容,
          mask: true, //显示透明蒙层，防止触摸穿透,
          success: res => {}
        });
        const session = qcloud.Session.get();
        if (session) {
          // 第二次登录
          // 或者本地已经有登录态
          // 可使用本函数更新登录态
          qcloud.loginWithCode({
            success: res => {
              // this.setData({ userInfo: res, logged: true });
              wx.setStorageSync("key", "value");
            },
            fail: err => {
              console.error(err);
            }
          });
        } else {
          // 首次登录
          qcloud.login({
            success: res => {
              console.log(res);
              wx.hideLoading();
              wx.setStorageSync("userInfo", res);
              var openId = res.openId;
              wx.setStorageSync("openId", openId);
              wx.navigateBack({});
            },
            fail: err => {
              console.log(err);
              wx.hideLoading();
              wx.navigateBack({});
            }
          });
        }
      }
    },
    computed: {}
  };
</script>
<style lang='scss' scoped>
  .login {
  width: 100%;
  height: 100%;
  background: #fff;
  box-sizing: border-box;
  padding-top: 1rpx;
  .logo {
    width: 230rpx;
    height: 80rpx;
    background: url('https://bookcover.yuewen.com/qdbimg/349573/1010734492/180') no-repeat;
    background-size: 100% 100%;
    margin: 200rpx auto 0 auto;
  }
  .login-btn {
    text-align: center;
    background: #b4a078;
    width: 90%;
    height: 80rpx;
    line-height: 80rpx;
    color: #fff;
    font-size: 28rpx;
    margin-top: 300rpx;
  }
}
</style>