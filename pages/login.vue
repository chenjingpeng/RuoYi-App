<template>
  <view class="login-container">
    <!-- Logo 与品牌 -->
    <view class="brand">
      <image class="logo" :src="globalConfig.appInfo.logo" mode="widthFix"></image>
      <text class="brand-name">若依移动端</text>
    </view>

    <!-- 标题区 -->
    <view class="header">
      <text class="eyebrow">SIGN IN</text>
      <text class="title">欢迎回来</text>
      <text class="subtitle">登录以继续使用</text>
    </view>

    <!-- 表单 -->
    <view class="form">
      <view class="input-item">
        <view class="iconfont icon-user input-icon"></view>
        <input v-model="loginForm.username" class="input" type="text" placeholder="账号" maxlength="30" />
      </view>

      <view class="input-item">
        <view class="iconfont icon-password input-icon"></view>
        <input v-model="loginForm.password" type="password" class="input" placeholder="密码" maxlength="20" />
      </view>

      <view class="input-item captcha-item" v-if="captchaEnabled">
        <view class="iconfont icon-code input-icon"></view>
        <input v-model="loginForm.code" type="number" class="input" placeholder="验证码" maxlength="4" />
        <image :src="codeUrl" @click="getCode" class="captcha-img"></image>
      </view>

      <button @click="handleLogin" class="login-btn">登录</button>

      <view class="footer">
        <text class="footer-text" v-if="register">没有账号？</text>
        <text @click="handleUserRegister" class="footer-link" v-if="register">立即注册</text>
      </view>

      <view class="agreements">
        <text class="footer-text">登录即代表同意</text>
        <text @click="handleUserAgrement" class="footer-link">《用户协议》</text>
        <text @click="handlePrivacy" class="footer-link">《隐私协议》</text>
      </view>
    </view>
  </view>
</template>

<script setup>
  import { ref, getCurrentInstance } from "vue"
  import { onLoad } from  "@dcloudio/uni-app"
  import { getToken } from '@/utils/auth'
  import { getCodeImg } from '@/api/login'
  import { useConfigStore, useUserStore } from '@/store'

  const { proxy } = getCurrentInstance()
  const globalConfig = useConfigStore().config
  const codeUrl = ref("")
  const captchaEnabled = ref(true)
  const register = ref(false)
  const loginForm = ref({
    username: "admin",
    password: "admin123",
    code: "",
    uuid: ""
  })

  function handleUserRegister() {
    proxy.$tab.redirectTo(`/pages/register`)
  }

  function handlePrivacy() {
    let site = globalConfig.appInfo.agreements[0]
    proxy.$tab.navigateTo(`/pages/common/webview/index?title=${site.title}&url=${site.url}`)
  }

  function handleUserAgrement() {
    let site = globalConfig.appInfo.agreements[1]
    proxy.$tab.navigateTo(`/pages/common/webview/index?title=${site.title}&url=${site.url}`)
  }

  function getCode() {
    getCodeImg().then(res => {
      captchaEnabled.value = res.captchaEnabled === undefined ? true : res.captchaEnabled
      if (captchaEnabled.value) {
        codeUrl.value = 'data:image/gif;base64,' + res.img
        loginForm.value.uuid = res.uuid
      }
    })
  }

  async function handleLogin() {
    if (loginForm.value.username === "") {
      proxy.$modal.msgError("请输入账号")
    } else if (loginForm.value.password === "") {
      proxy.$modal.msgError("请输入密码")
    } else if (loginForm.value.code === "" && captchaEnabled.value) {
      proxy.$modal.msgError("请输入验证码")
    } else {
      proxy.$modal.loading("登录中，请耐心等待...")
      pwdLogin()
    }
  }

  async function pwdLogin() {
    useUserStore().login(loginForm.value).then(() => {
      proxy.$modal.closeLoading()
      loginSuccess()
    }).catch(() => {
      if (captchaEnabled.value) {
        getCode()
      }
    })
  }

  function loginSuccess() {
    useUserStore().getInfo().then(res => {
      proxy.$tab.reLaunch('/pages/index')
    })
  }

  onLoad(() => {
    if (getToken()) {
      proxy.$tab.reLaunch('/pages/index')
    }
  })

  getCode()
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .login-container {
    min-height: 100vh;
    padding: 80px 24px 24px;
  }

  /* 品牌 */
  .brand {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 48px;
  }

  .logo {
    width: 32px;
    height: 32px;
    border-radius: 6px;
  }

  .brand-name {
    font-size: 15px;
    font-weight: 600;
    color: #f7f8f8;
    letter-spacing: -0.01em;
  }

  /* 头部 */
  .header {
    margin-bottom: 40px;
  }

  .eyebrow {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #5e6ad2;
    margin-bottom: 12px;
  }

  .title {
    display: block;
    font-size: 32px;
    font-weight: 700;
    color: #f7f8f8;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 8px;
  }

  .subtitle {
    display: block;
    font-size: 14px;
    color: #8a8f98;
  }

  /* 表单 */
  .form {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .input-item {
    display: flex;
    align-items: center;
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 10px;
    height: 48px;
    padding: 0 14px;
    transition: border-color 0.15s;
  }

  .input-item:focus-within {
    border-color: #5e6ad2;
  }

  .input-icon {
    font-size: 18px;
    color: #62666d;
    margin-right: 10px;
  }

  .input {
    flex: 1;
    height: 100%;
    font-size: 15px;
    color: #f7f8f8;
    background: transparent;
  }

  .input::placeholder {
    color: #62666d;
  }

  .captcha-item .input {
    flex: 0 1 auto;
    width: 60%;
  }

  .captcha-img {
    height: 32px;
    width: 88px;
    border-radius: 4px;
  }

  .login-btn {
    margin-top: 16px;
    height: 48px;
    line-height: 48px;
    background-color: #5e6ad2;
    color: #ffffff;
    border: none;
    border-radius: 10px;
    font-size: 15px;
    font-weight: 600;
    letter-spacing: 0.01em;
  }

  .login-btn::after {
    border: none;
  }

  .footer {
    display: flex;
    justify-content: center;
    gap: 4px;
    margin-top: 20px;
    font-size: 13px;
  }

  .agreements {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 4px;
    margin-top: 12px;
    font-size: 12px;
  }

  .footer-text {
    color: #62666d;
  }

  .footer-link {
    color: #5e6ad2;
  }
</style>
