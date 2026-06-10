<template>
  <view class="home-container">
    <!-- 品牌展示卡片 -->
    <view class="brand-card">
      <image class="logo" src="@/static/logo.png" mode="aspectFit"></image>
      <text class="app-name">若依移动端</text>
      <text class="app-version">v1.2.0</text>
      <text class="app-desc">开源快速开发平台</text>
    </view>

    <!-- 快捷入口卡片 -->
    <view class="quick-access">
      <text class="section-title">快捷入口</text>
      <view class="access-grid">
        <view class="access-item" @click="navigateTo('/pages/work/index')">
          <view class="access-icon">
            <uni-icons type="gear-filled" size="24" color="#5e6ad2"></uni-icons>
          </view>
          <text class="access-label">工作台</text>
        </view>
        <view class="access-item" @click="navigateTo('/pages/mine/index')">
          <view class="access-icon">
            <uni-icons type="person-filled" size="24" color="#5e6ad2"></uni-icons>
          </view>
          <text class="access-label">个人中心</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
  function navigateTo(url) {
    uni.navigateTo({ url })
  }
</script>

<style scoped>
  page {
    background-color: #010102;
  }

  .home-container {
    padding: 24px 16px;
  }

  .brand-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 40px 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 16px;
  }

  .logo {
    width: 120rpx;
    height: 120rpx;
    margin-bottom: 16px;
  }

  .app-name {
    font-size: 28px;
    font-weight: 600;
    color: #f7f8f8;
    font-family: 'Inter', 'SF Pro Display', -apple-system, 'system-ui', sans-serif;
    margin-bottom: 4px;
  }

  .app-version {
    font-size: 13px;
    color: #8a8f98;
    margin-bottom: 8px;
  }

  .app-desc {
    font-size: 14px;
    color: #d0d6e0;
  }

  .quick-access {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 20px 16px;
  }

  .section-title {
    font-size: 16px;
    font-weight: 600;
    color: #f7f8f8;
    margin-bottom: 16px;
    display: block;
  }

  .access-grid {
    display: flex;
    gap: 12px;
  }

  .access-item {
    flex: 1;
    background-color: #141516;
    border: 1px solid #23252a;
    border-radius: 8px;
    padding: 16px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
  }

  .access-icon {
    width: 44px;
    height: 44px;
    background-color: #18191a;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .access-label {
    font-size: 13px;
    color: #d0d6e0;
  }
</style>
