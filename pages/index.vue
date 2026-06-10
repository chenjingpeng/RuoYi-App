<template>
  <view class="home-container">
    <!-- 顶部品牌区 -->
    <view class="hero">
      <view class="hero-eyebrow">OPEN SOURCE · MOBILE FRAMEWORK</view>
      <text class="hero-title">若依移动端</text>
      <text class="hero-subtitle">为开发者打造的高效、优雅、可靠的移动端开发框架</text>
    </view>

    <!-- 版本与统计卡片 -->
    <view class="stat-card">
      <view class="stat-item">
        <text class="stat-value">v1.2.0</text>
        <text class="stat-label">当前版本</text>
      </view>
      <view class="stat-divider"></view>
      <view class="stat-item">
        <text class="stat-value">100+</text>
        <text class="stat-label">功能模块</text>
      </view>
      <view class="stat-divider"></view>
      <view class="stat-item">
        <text class="stat-value">MIT</text>
        <text class="stat-label">开源协议</text>
      </view>
    </view>

    <!-- 特性列表 -->
    <view class="feature-section">
      <text class="section-label">FEATURES</text>
      <view class="feature-list">
        <view class="feature-item">
          <view class="feature-dot"></view>
          <text class="feature-text">完整的前后端分离架构，开箱即用</text>
        </view>
        <view class="feature-item">
          <view class="feature-dot"></view>
          <text class="feature-text">基于 uni-app 跨端框架，一套代码多端运行</text>
        </view>
        <view class="feature-item">
          <view class="feature-dot"></view>
          <text class="feature-text">细粒度权限控制，菜单、按钮级授权</text>
        </view>
        <view class="feature-item">
          <view class="feature-dot"></view>
          <text class="feature-text">代码生成器一键生成前后端代码</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
</script>

<style scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .home-container {
    padding: 48px 24px 24px;
  }

  /* Hero 头部 */
  .hero {
    margin-bottom: 32px;
  }

  .hero-eyebrow {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #5e6ad2;
    margin-bottom: 12px;
  }

  .hero-title {
    display: block;
    font-size: 32px;
    font-weight: 700;
    color: #f7f8f8;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 12px;
  }

  .hero-subtitle {
    display: block;
    font-size: 15px;
    color: #8a8f98;
    line-height: 1.5;
    max-width: 90%;
  }

  /* 统计卡片 */
  .stat-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 20px 0;
    display: flex;
    align-items: center;
    margin-bottom: 32px;
  }

  .stat-item {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
  }

  .stat-value {
    font-size: 18px;
    font-weight: 600;
    color: #f7f8f8;
    letter-spacing: -0.01em;
  }

  .stat-label {
    font-size: 11px;
    color: #8a8f98;
  }

  .stat-divider {
    width: 1px;
    height: 24px;
    background-color: #23252a;
  }

  /* 特性区 */
  .section-label {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #8a8f98;
    margin-bottom: 16px;
  }

  .feature-section {
    padding: 0 4px;
  }

  .feature-list {
    display: flex;
    flex-direction: column;
  }

  .feature-item {
    display: flex;
    align-items: flex-start;
    padding: 14px 0;
    border-top: 1px solid #18191a;
  }

  .feature-dot {
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background-color: #5e6ad2;
    margin-top: 8px;
    margin-right: 12px;
    flex-shrink: 0;
  }

  .feature-text {
    font-size: 14px;
    color: #d0d6e0;
    line-height: 1.5;
  }
</style>
