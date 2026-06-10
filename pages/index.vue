<template>
  <view class="content">
    <image class="logo" src="@/static/logo.png"></image>
    <view class="text-area">
      <text class="title">Hello RuoYi</text>
    </view>
  </view>
</template>

<style scoped>
  page {
    background-color: #010102;
  }

  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: #010102;
  }

  .logo {
    height: 200rpx;
    width: 200rpx;
    margin-top: 200rpx;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 50rpx;
  }

  .text-area {
    display: flex;
    justify-content: center;
  }

  .title {
    font-size: 28px;
    font-weight: 600;
    font-family: 'Inter', 'SF Pro Display', -apple-system, 'system-ui', sans-serif;
    color: #f7f8f8;
  }
</style>
