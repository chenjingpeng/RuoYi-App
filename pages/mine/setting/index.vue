<template>
  <view class="setting-container">
    <text class="group-label">账号</text>
    <view class="menu-group">
      <view class="menu-cell list-cell-arrow" @click="handleToPwd">
        <view class="iconfont icon-password menu-icon"></view>
        <text class="menu-label">修改密码</text>
      </view>
    </view>

    <text class="group-label">通用</text>
    <view class="menu-group">
      <view class="menu-cell list-cell-arrow" @click="handleToUpgrade">
        <view class="iconfont icon-refresh menu-icon"></view>
        <text class="menu-label">检查更新</text>
      </view>
      <view class="menu-cell list-cell-arrow" @click="handleCleanTmp">
        <view class="iconfont icon-clean menu-icon"></view>
        <text class="menu-label">清理缓存</text>
      </view>
    </view>

    <button class="logout-btn" @click="handleLogout">退出登录</button>
  </view>
</template>

<script setup>
  import { useUserStore } from '@/store'
  import { getCurrentInstance } from "vue"

  const { proxy } = getCurrentInstance()

  function handleToPwd() {
    proxy.$tab.navigateTo('/pages/mine/pwd/index')
  }

  function handleToUpgrade() {
    proxy.$modal.showToast('模块建设中~')
  }

  function handleCleanTmp() {
    proxy.$modal.showToast('模块建设中~')
  }

  function handleLogout() {
    proxy.$modal.confirm('确定注销并退出系统吗？').then(() => {
      useUserStore().logOut().then(() => {}).finally(() => {
        proxy.$tab.reLaunch('/pages/index')
      })
    })
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .setting-container {
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

  .group-label + .menu-group {
    margin-bottom: 24px;
  }

  .menu-group {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    overflow: hidden;
  }

  .menu-cell {
    position: relative;
    display: flex;
    align-items: center;
    padding: 14px 16px;
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

  .logout-btn {
    margin-top: 32px;
    width: 100%;
    height: 48px;
    line-height: 48px;
    background-color: transparent;
    color: #dd524d;
    border: 1px solid #23252a;
    border-radius: 10px;
    font-size: 14px;
    font-weight: 500;
  }

  .logout-btn::after {
    border: none;
  }
</style>
