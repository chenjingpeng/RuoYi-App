<template>
  <view class="mine-container">
    <!-- 用户信息卡片 -->
    <view class="user-card">
      <view class="user-info">
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
      <view class="edit-btn" @click="handleToInfo">
        <text class="edit-text">个人信息</text>
        <view class="iconfont icon-right edit-arrow"></view>
      </view>
    </view>

    <!-- 快捷操作卡片 -->
    <view class="action-card">
      <view class="action-item" @click="handleJiaoLiuQun">
        <view class="action-icon primary">
          <view class="iconfont icon-friendfill"></view>
        </view>
        <text class="action-label">交流群</text>
      </view>
      <view class="action-item" @click="handleBuilding">
        <view class="action-icon primary">
          <view class="iconfont icon-service"></view>
        </view>
        <text class="action-label">在线客服</text>
      </view>
      <view class="action-item" @click="handleBuilding">
        <view class="action-icon primary">
          <view class="iconfont icon-community"></view>
        </view>
        <text class="action-label">反馈社区</text>
      </view>
      <view class="action-item" @click="handleBuilding">
        <view class="action-icon primary">
          <view class="iconfont icon-dianzan"></view>
        </view>
        <text class="action-label">点赞我们</text>
      </view>
    </view>

    <!-- 菜单列表 -->
    <view class="menu-section">
      <view class="menu-list">
        <view class="list-cell list-cell-arrow" @click="handleToEditInfo">
          <view class="menu-item-box">
            <view class="iconfont icon-user menu-icon"></view>
            <view>编辑资料</view>
          </view>
        </view>
        <view class="list-cell list-cell-arrow" @click="handleHelp">
          <view class="menu-item-box">
            <view class="iconfont icon-help menu-icon"></view>
            <view>常见问题</view>
          </view>
        </view>
        <view class="list-cell list-cell-arrow" @click="handleAbout">
          <view class="menu-item-box">
            <view class="iconfont icon-aixin menu-icon"></view>
            <view>关于我们</view>
          </view>
        </view>
        <view class="list-cell list-cell-arrow" @click="handleToSetting">
          <view class="menu-item-box">
            <view class="iconfont icon-setting menu-icon"></view>
            <view>应用设置</view>
          </view>
        </view>
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
  const windowHeight = computed(() => uni.getSystemInfoSync().windowHeight - 50)

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
      
  function handleJiaoLiuQun() {
    proxy.$modal.showToast('QQ群：①133713780(满)、②146013835(满)、③189091635')
  }
      
  function handleBuilding() {
    proxy.$modal.showToast('模块建设中~')
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
  }

  .mine-container {
    padding: 16px;
  }

  /* 用户信息卡片 */
  .user-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 20px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 12px;
  }

  .user-info {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .avatar-placeholder {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background-color: #18191a;
    border: 2px solid #23252a;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .avatar-icon {
    font-size: 28px;
    color: #8a8f98;
  }

  .avatar {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    border: 2px solid #23252a;
  }

  .user-meta {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .login-text {
    font-size: 16px;
    color: #5e6ad2;
  }

  .username {
    font-size: 18px;
    font-weight: 600;
    color: #f7f8f8;
  }

  .user-role {
    font-size: 12px;
    color: #8a8f98;
  }

  .edit-btn {
    display: flex;
    align-items: center;
    gap: 4px;
    cursor: pointer;
  }

  .edit-text {
    font-size: 13px;
    color: #8a8f98;
  }

  .edit-arrow {
    font-size: 12px;
    color: #8a8f98;
  }

  /* 快捷操作卡片 */
  .action-card {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    padding: 16px;
    display: flex;
    justify-content: space-around;
    margin-bottom: 12px;
  }

  .action-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    cursor: pointer;
  }

  .action-icon {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .action-icon.primary {
    background-color: rgba(94, 106, 210, 0.15);
  }

  .action-icon .iconfont {
    font-size: 20px;
    color: #5e6ad2;
  }

  .action-label {
    font-size: 12px;
    color: #d0d6e0;
  }

  /* 菜单区域 */
  .menu-section {
    background-color: #0f1011;
    border: 1px solid #23252a;
    border-radius: 12px;
    overflow: hidden;
  }

  .menu-list {
    margin: 0;
  }
</style>
