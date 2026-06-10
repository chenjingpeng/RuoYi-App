<template>
  <view class="mine-container">
    <!-- 用户信息头部 -->
    <view class="user-header">
      <view v-if="!avatar" class="avatar-placeholder">
        <view class="iconfont icon-people avatar-icon"></view>
      </view>
      <image v-if="avatar" @click="handleToAvatar" :src="avatar" class="avatar" mode="aspectFill"></image>
      <view class="user-meta">
        <text v-if="!name" @click="handleToLogin" class="login-text">点击登录</text>
        <text v-if="name" class="username">{{ name }}</text>
        <text v-if="name" class="user-role">超级管理员</text>
      </view>
    </view>

    <!-- 菜单列表 -->
    <view class="menu-group">
      <view class="menu-cell list-cell-arrow" @click="handleToEditInfo">
        <view class="iconfont icon-user menu-icon"></view>
        <text class="menu-label">编辑资料</text>
      </view>
      <view class="menu-cell list-cell-arrow" @click="handleToInfo">
        <view class="iconfont icon-people menu-icon"></view>
        <text class="menu-label">个人信息</text>
      </view>
      <view class="menu-cell list-cell-arrow" @click="handleHelp">
        <view class="iconfont icon-help menu-icon"></view>
        <text class="menu-label">常见问题</text>
      </view>
      <view class="menu-cell list-cell-arrow" @click="handleAbout">
        <view class="iconfont icon-aixin menu-icon"></view>
        <text class="menu-label">关于我们</text>
      </view>
    </view>

    <view class="menu-group">
      <view class="menu-cell list-cell-arrow" @click="handleToSetting">
        <view class="iconfont icon-setting menu-icon"></view>
        <text class="menu-label">应用设置</text>
      </view>
    </view>
  </view>
</template>

<script setup>
  import { useUserStore } from '@/store'
  import { computed , getCurrentInstance } from "vue"

  const { proxy } = getCurrentInstance()
  const name = useUserStore().name
  const avatar = computed(() => useUserStore().avatar)

  function handleToInfo() {
    proxy.$tab.navigateTo('/pages/mine/info/index')
  }

  function handleToEditInfo() {
    proxy.$tab.navigateTo('/pages/mine/info/edit')
  }

  function handleToSetting() {
    proxy.$tab.navigateTo('/pages/mine/setting/index')
  }

  function handleToLogin() {
    proxy.$tab.reLaunch('/pages/login')
  }

  function handleToAvatar() {
    proxy.$tab.navigateTo('/pages/mine/avatar/index')
  }

  function handleHelp() {
    proxy.$tab.navigateTo('/pages/mine/help/index')
  }

  function handleAbout() {
    proxy.$tab.navigateTo('/pages/mine/about/index')
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .mine-container {
    padding: 32px 16px 16px;
  }

  /* 用户信息头部 */
  .user-header {
    display: flex;
    align-items: center;
    padding: 16px 8px 32px;
  }

  .avatar-placeholder {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background-color: #0f1011;
    border: 1px solid #23252a;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .avatar-icon {
    font-size: 26px;
    color: #8a8f98;
  }

  .avatar {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    border: 1px solid #23252a;
    flex-shrink: 0;
  }

  .user-meta {
    display: flex;
    flex-direction: column;
    gap: 4px;
    margin-left: 16px;
  }

  .login-text {
    font-size: 18px;
    font-weight: 600;
    color: #5e6ad2;
  }

  .username {
    font-size: 20px;
    font-weight: 600;
    color: #f7f8f8;
    letter-spacing: -0.01em;
  }

  .user-role {
    font-size: 12px;
    color: #8a8f98;
  }

  /* 菜单分组 */
  .menu-group {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    margin-bottom: 8px;
    overflow: hidden;
  }

  .menu-cell {
    position: relative;
    display: flex;
    align-items: center;
    padding: 16px 16px;
    border-top: 1px solid #18191a;
  }

  .menu-group .menu-cell:first-child {
    border-top: none;
  }

  .menu-icon {
    font-size: 16px;
    color: #8a8f98;
    margin-right: 12px;
  }

  .menu-label {
    font-size: 14px;
    color: #f7f8f8;
  }

  /* 列表箭头 */
  .list-cell-arrow::before {
    content: ' ';
    height: 8px;
    width: 8px;
    border-width: 1.5px 1.5px 0 0;
    border-color: #62666d;
    border-style: solid;
    transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
    position: absolute;
    top: 50%;
    margin-top: -4px;
    right: 16px;
  }
</style>
