<template>
  <view class="register-container">
    <!-- 标题区 -->
    <view class="header">
      <text class="eyebrow">SIGN UP</text>
      <text class="title">创建账号</text>
      <text class="subtitle">填写以下信息完成注册</text>
    </view>

    <!-- 表单 -->
    <view class="form">
      <view class="input-item">
        <view class="iconfont icon-user input-icon"></view>
        <input v-model="registerForm.username" class="input" type="text" placeholder="账号" maxlength="30" />
      </view>

      <view class="input-item">
        <view class="iconfont icon-password input-icon"></view>
        <input v-model="registerForm.password" type="password" class="input" placeholder="密码" maxlength="20" />
      </view>

      <view class="input-item">
        <view class="iconfont icon-password input-icon"></view>
        <input v-model="registerForm.confirmPassword" type="password" class="input" placeholder="确认密码" maxlength="20" />
      </view>

      <button @click="handleRegister" class="register-btn">注册</button>

      <view class="agreements">
        <text class="footer-text">注册即代表同意</text>
        <text @click="handleUserAgrement" class="footer-link">《用户协议》</text>
        <text @click="handlePrivacy" class="footer-link">《隐私协议》</text>
      </view>
    </view>
  </view>
</template>

<script setup>
  import { reactive, getCurrentInstance } from "vue"
  import { useConfigStore } from '@/store'
  import { register } from '@/api/login'

  const { proxy } = getCurrentInstance()
  const globalConfig = useConfigStore().config

  const registerForm = reactive({
    username: "",
    password: "",
    confirmPassword: ""
  })

  const rules = {
    username: [
      { required: true, trigger: 'blur', message: '请输入用户名' },
      { min: 2, max: 20, message: '长度在 2 到 20 个字符', trigger: 'blur' }
    ],
    password: [
      { required: true, trigger: 'blur', message: '请输入密码' },
      { min: 5, max: 20, message: '长度在 5 到 20 个字符', trigger: 'blur' }
    ],
    confirmPassword: [
      { required: true, trigger: 'blur', message: '请再次输入密码' },
      {
        validator: (rule, value, callback) => {
          if (value !== registerForm.password) {
            callback(new Error('两次输入的密码不一致'))
          } else {
            callback()
          }
        },
        trigger: 'blur'
      }
    ]
  }

  function handleUserAgrement() {
    let site = globalConfig.appInfo.agreements[1]
    proxy.$tab.navigateTo(`/pages/common/webview/index?title=${site.title}&url=${site.url}`)
  }

  function handlePrivacy() {
    let site = globalConfig.appInfo.agreements[0]
    proxy.$tab.navigateTo(`/pages/common/webview/index?title=${site.title}&url=${site.url}`)
  }

  function handleRegister() {
    if (registerForm.username === "") {
      proxy.$modal.msgError("请输入账号")
      return
    }
    if (registerForm.password === "") {
      proxy.$modal.msgError("请输入密码")
      return
    }
    if (registerForm.confirmPassword === "") {
      proxy.$modal.msgError("请再次输入密码")
      return
    }
    if (registerForm.password !== registerForm.confirmPassword) {
      proxy.$modal.msgError("两次输入的密码不一致")
      return
    }
    register(registerForm).then(() => {
      proxy.$modal.msgSuccess("注册成功，请登录")
      proxy.$tab.reLaunch('/pages/login')
    })
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .register-container {
    min-height: 100vh;
    padding: 80px 24px 24px;
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

  .register-btn {
    margin-top: 16px;
    height: 48px;
    line-height: 48px;
    background-color: #5e6ad2;
    color: #ffffff;
    border: none;
    border-radius: 10px;
    font-size: 15px;
    font-weight: 600;
  }

  .register-btn::after {
    border: none;
  }

  .agreements {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 4px;
    margin-top: 20px;
    font-size: 12px;
  }

  .footer-text {
    color: #62666d;
  }

  .footer-link {
    color: #5e6ad2;
  }
</style>
