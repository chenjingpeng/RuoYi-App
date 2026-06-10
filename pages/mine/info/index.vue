<template>
  <view class="container">
    <text class="group-label">基本信息</text>
    <view class="info-group">
      <view class="info-cell">
        <view class="iconfont icon-user info-icon"></view>
        <text class="info-label">昵称</text>
        <text class="info-value">{{ user.nickName }}</text>
      </view>
      <view class="info-cell">
        <view class="iconfont icon-phone info-icon"></view>
        <text class="info-label">手机号码</text>
        <text class="info-value">{{ user.phonenumber }}</text>
      </view>
      <view class="info-cell">
        <view class="iconfont icon-email info-icon"></view>
        <text class="info-label">邮箱</text>
        <text class="info-value">{{ user.email }}</text>
      </view>
      <view class="info-cell">
        <view class="iconfont icon-auth info-icon"></view>
        <text class="info-label">岗位</text>
        <text class="info-value">{{ postGroup }}</text>
      </view>
      <view class="info-cell">
        <view class="iconfont icon-staff info-icon"></view>
        <text class="info-label">角色</text>
        <text class="info-value">{{ roleGroup }}</text>
      </view>
      <view class="info-cell">
        <view class="iconfont icon-calendar info-icon"></view>
        <text class="info-label">创建日期</text>
        <text class="info-value">{{ user.createTime }}</text>
      </view>
    </view>
  </view>
</template>

<script setup>
  import { getUserProfile } from "@/api/system/user"
  import { ref } from "vue"

  const user = ref({})
  const roleGroup = ref("")
  const postGroup = ref("")

  function getUser() {
    getUserProfile().then(response => {
      user.value = response.data
      roleGroup.value = response.roleGroup
      postGroup.value = response.postGroup
    })
  }

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

  .info-group {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    overflow: hidden;
  }

  .info-cell {
    display: flex;
    align-items: center;
    padding: 14px 16px;
    border-top: 1px solid #18191a;
  }

  .info-group .info-cell:first-child {
    border-top: none;
  }

  .info-icon {
    font-size: 16px;
    color: #8a8f98;
    margin-right: 12px;
  }

  .info-label {
    font-size: 14px;
    color: #d0d6e0;
    flex: 1;
  }

  .info-value {
    font-size: 13px;
    color: #8a8f98;
  }
</style>
