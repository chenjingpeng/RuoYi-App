<template>
  <view class="work-container">
    <!-- Hero 区域 -->
    <view class="hero">
      <view class="hero-eyebrow">DASHBOARD</view>
      <text class="hero-title">欢迎使用若依</text>
      <text class="hero-subtitle">开源快速开发平台，全系列可免费商用无需授权</text>
    </view>

    <!-- 系统管理分组 -->
    <view class="group">
      <text class="group-label">系统管理</text>
      <view class="grid-card">
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="person-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">用户管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="staff-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">角色管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="color" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">菜单管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="settings-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">部门管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="auth-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">岗位管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="bars" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">字典管理</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="gear-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">参数设置</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="chat-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">通知公告</text>
        </view>
        <view class="grid-item" @click="handleClick">
          <view class="grid-icon-wrap primary">
            <uni-icons type="wallet-filled" size="20" color="#5e6ad2"></uni-icons>
          </view>
          <text class="grid-label">日志管理</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
  import { getCurrentInstance } from "vue"

  const { proxy } = getCurrentInstance()

  function handleClick() {
    proxy.$modal.showToast('模块建设中~')
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .work-container {
    padding: 32px 16px 16px;
  }

  /* Hero */
  .hero {
    margin-bottom: 32px;
    padding: 0 8px;
  }

  .hero-eyebrow {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #5e6ad2;
    margin-bottom: 8px;
  }

  .hero-title {
    display: block;
    font-size: 28px;
    font-weight: 700;
    color: #f7f8f8;
    letter-spacing: -0.02em;
    line-height: 1.2;
    margin-bottom: 8px;
  }

  .hero-subtitle {
    display: block;
    font-size: 14px;
    color: #8a8f98;
    line-height: 1.5;
  }

  /* 分组 */
  .group {
    margin-bottom: 24px;
  }

  .group-label {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #8a8f98;
    margin-bottom: 12px;
    padding: 0 8px;
  }

  /* 网格卡片 */
  .grid-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 4px 0;
    display: flex;
    flex-wrap: wrap;
  }

  .grid-item {
    width: 25%;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    padding: 16px 4px;
    box-sizing: border-box;
  }

  .grid-icon-wrap {
    width: 36px;
    height: 36px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .grid-icon-wrap.primary {
    background-color: rgba(94, 106, 210, 0.12);
  }

  .grid-label {
    font-size: 12px;
    color: #d0d6e0;
  }
</style>
