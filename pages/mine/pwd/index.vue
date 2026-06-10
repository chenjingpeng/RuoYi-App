<template>
  <view class="container">
    <text class="group-label">修改密码</text>
    <view class="form-card">
      <uni-forms ref="form" :value="user" labelWidth="80px">
        <uni-forms-item name="oldPassword" label="旧密码">
          <uni-easyinput type="password" v-model="user.oldPassword" placeholder="请输入旧密码" />
        </uni-forms-item>
        <uni-forms-item name="newPassword" label="新密码">
          <uni-easyinput type="password" v-model="user.newPassword" placeholder="请输入新密码" />
        </uni-forms-item>
        <uni-forms-item name="confirmPassword" label="确认密码">
          <uni-easyinput type="password" v-model="user.confirmPassword" placeholder="请确认新密码" />
        </uni-forms-item>
      </uni-forms>
    </view>

    <button class="submit-btn" @click="submit">更新密码</button>
  </view>
</template>

<script setup>
  import { updateUserPwd } from "@/api/system/user"
  import { ref, reactive , getCurrentInstance } from "vue"
  import { onReady } from  "@dcloudio/uni-app"

  const { proxy } = getCurrentInstance()
  const user = reactive({
    oldPassword: undefined,
    newPassword: undefined,
    confirmPassword: undefined
  })
  const rules = ref({
    oldPassword: {
      rules: [{
        required: true,
        errorMessage: '旧密码不能为空'
      }]
    },
    newPassword: {
      rules: [{
        required: true,
        errorMessage: '新密码不能为空',
      }, {
        minLength: 6,
        maxLength: 20,
        errorMessage: '长度在 6 到 20 个字符'
      }]
    },
    confirmPassword: {
      rules: [{
        required: true,
        errorMessage: '确认密码不能为空'
      }, {
        validateFunction: (rule, value, data) => user.newPassword === value,
        errorMessage: '两次输入的密码不一致'
      }]
    }
  })

  onReady(() => {
    proxy.$refs.form.setRules(rules.value)
  })

  function submit() {
    proxy.$refs.form.validate().then(res => {
      updateUserPwd(user.oldPassword, user.newPassword).then(response => {
        proxy.$modal.msgSuccess("修改成功")
      })
    })
  }
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
