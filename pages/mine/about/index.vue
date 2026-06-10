<template>
  <view class="about-container">
    <!-- 品牌头部 -->
    <view class="hero">
      <image class="logo" src="/static/logo200.png" mode="widthFix"></image>
      <text class="brand-name">若依移动端</text>
      <text class="version">Version {{ version }}</text>
    </view>

    <!-- 详情分组 -->
    <text class="group-label">关于</text>
    <view class="menu-group">
      <view class="menu-cell list-cell-arrow">
        <text class="menu-label">版本信息</text>
        <text class="menu-value">v{{ version }}</text>
      </view>
      <view class="menu-cell list-cell-arrow">
        <text class="menu-label">官方邮箱</text>
        <text class="menu-value">ruoyi@xx.com</text>
      </view>
      <view class="menu-cell list-cell-arrow">
        <text class="menu-label">服务热线</text>
        <text class="menu-value">400-999-9999</text>
      </view>
      <view class="menu-cell list-cell-arrow">
        <text class="menu-label">公司网站</text>
        <text class="menu-value">{{ url }}</text>
      </view>
    </view>

    <text class="copyright">Copyright © 2025 ruoyi.vip</text>
  </view>
</template>

<script setup>
  import { useConfigStore } from '@/store'

  const url = useConfigStore().config.appInfo.site_url
  const version = useConfigStore().config.appInfo.version
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
    font-family: 'Inter', -apple-system, 'system-ui', sans-serif;
  }

  .about-container {
    padding: 48px 16px 24px;
  }

  /* Hero */
  .hero {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 40px;
  }

  .logo {
    width: 64px;
    height: 64px;
    margin-bottom: 16px;
  }

  .brand-name {
    font-size: 18px;
    font-weight: 600;
    color: #f7f8f8;
    letter-spacing: -0.01em;
    margin-bottom: 4px;
  }

  .version {
    font-size: 12px;
    color: #62666d;
  }

  /* 分组 */
  .group-label {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.12em;
    color: #62666d;
    margin: 0 8px 8px;
  }

  .menu-group {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    overflow: hidden;
    margin-bottom: 24px;
  }

  .menu-cell {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 14px 16px;
    border-top: 1px solid #18191a;
  }

  .menu-group .menu-cell:first-child {
    border-top: none;
  }

  .menu-label {
    font-size: 14px;
    color: #f7f8f8;
  }

  .menu-value {
    font-size: 13px;
    color: #8a8f98;
    padding-right: 16px;
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

  .copyright {
    display: block;
    text-align: center;
    font-size: 11px;
    color: #62666d;
    margin-top: 24px;
  }
</style>
