<template>
  <view class="setting-container" :style="{height: `${windowHeight}px`}">
    <view class="menu-list">
      <view class="list-cell list-cell-arrow" @click="handleToPwd">
        <view class="menu-item-box">
          <view class="iconfont icon-password menu-icon"></view>
          <view>修改密码</view>
        </view>
      </view>
      <view class="list-cell list-cell-arrow" @click="handleToUpgrade">
        <view class="menu-item-box">
          <view class="iconfont icon-refresh menu-icon"></view>
          <view>检查更新</view>
        </view>
      </view>
      <view class="list-cell list-cell-arrow" @click="handleCleanTmp">
        <view class="menu-item-box">
          <view class="iconfont icon-clean menu-icon"></view>
          <view>清理缓存</view>
        </view>
      </view>
    </view>
      <view class="logout-section">
      <button class="btn-primary logout-btn" @click="handleLogout">退出登录</button>
    </view>
  </view>
</template>

<script setup>
  import { useUserStore } from '@/store'
  import { ref, computed , getCurrentInstance } from "vue"

  const { proxy } = getCurrentInstance()
  const windowHeight = computed(() => uni.getSystemInfoSync().windowHeight - 50)

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
      useUserStore().logOut().then(() => {}).finally(()=>{
        proxy.$tab.reLaunch('/pages/index')
      })
    })
  }
</script>

<style lang="scss" scoped>
  page {
    background-color: #010102;
  }

  .logout-section {
    margin: 30rpx;
  }
  .logout-btn {
    width: 100%;
    height: 44px;
    line-height: 44px;
    font-size: 16px;
  }
</style>
