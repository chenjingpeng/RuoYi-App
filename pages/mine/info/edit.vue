<template>
  <view class="container">
    <text class="group-label">账号信息</text>
    <view class="form-card">
      <uni-forms ref="form" :model="user" labelWidth="80px">
        <uni-forms-item label="用户昵称" name="nickName">
          <uni-easyinput v-model="user.nickName" placeholder="请输入昵称" />
        </uni-forms-item>
        <uni-forms-item label="手机号码" name="phonenumber">
          <uni-easyinput v-model="user.phonenumber" placeholder="请输入手机号码" />
        </uni-forms-item>
        <uni-forms-item label="邮箱" name="email">
          <uni-easyinput v-model="user.email" placeholder="请输入邮箱" />
        </uni-forms-item>
        <uni-forms-item label="性别" name="sex" required>
          <uni-data-checkbox v-model="user.sex" :localdata="sexs" />
        </uni-forms-item>
      </uni-forms>
    </view>

    <button class="submit-btn" @click="submit">保存修改</button>
  </view>
</template>

<script setup>
  import { getUserProfile, updateUserProfile } from "@/api/system/user"
  import { ref , getCurrentInstance } from "vue"
  import { onReady } from  "@dcloudio/uni-app"

  const { proxy } = getCurrentInstance()
  const user = ref({
    nickName: "",
    phonenumber: "",
    email: "",
    sex: ""
  })
  const sexs = [{
    text: '男',
    value: "0"
  }, {
    text: '女',
    value: "1"
  }]
  const rules = ref({
    nickName: {
      rules: [{
        required: true,
        errorMessage: '用户昵称不能为空'
      }]
    },
    phonenumber: {
      rules: [{
        required: true,
        errorMessage: '手机号码不能为空'
      }, {
        pattern: /^1[3|4|5|6|7|8|9][0-9]\d{8}$/,
        errorMessage: '请输入正确的手机号码'
      }]
    },
    email: {
      rules: [{
        required: true,
        errorMessage: '邮箱地址不能为空'
      }, {
        format: 'email',
        errorMessage: '请输入正确的邮箱地址'
      }]
    }
  })

  function getUser() {
    getUserProfile().then(response => {
      user.value = response.data
    })
  }

  function submit() {
    proxy.$refs.form.validate().then(res => {
      updateUserProfile(user.value).then(response => {
        proxy.$modal.msgSuccess("修改成功")
      })
    })
  }

  onReady(() => {
    proxy.$refs.form.setRules(rules.value)
  })

  getUser()
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .container {
    padding: 32px 16px 24px;
  }

  .group-label {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #62666d;
    margin: 0 8px 8px;
  }

  .form-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 8px 16px;
  }

  .submit-btn {
    margin-top: 24px;
    width: 100%;
    height: 48px;
    line-height: 48px;
    background-color: #5e6ad2;
    color: #ffffff;
    border: none;
    border-radius: 10px;
    font-size: 15px;
    font-weight: 600;
  }

  .submit-btn::after {
    border: none;
  }

  /* uni-easyinput 深色覆盖 */
  ::v-deep .uni-easyinput__content {
    background-color: transparent !important;
    border-color: transparent !important;
  }

  ::v-deep .uni-easyinput__content-input {
    color: #f7f8f8 !important;
    text-align: right;
  }

  ::v-deep .uni-forms-item__label {
    color: #d0d6e0 !important;
  }
</style>
