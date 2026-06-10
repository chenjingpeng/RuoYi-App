# Tasks

- [x] Task 1: 更新 uni.scss 全局设计令牌
  - [x] 将 uni.scss 中所有样式变量替换为 DESIGN.md 定义的 Linear 设计令牌（颜色、排版、圆角、间距）
  - [x] 保留 uni-app 必要的变量前缀（$uni-），同时新增 $linear- 前缀变量供页面引用

- [x] Task 2: 更新 global.scss 全局辅助样式
  - [x] 移除白色背景的全局样式（.list-cell, .menu-list 等）
  - [x] 新增暗黑画布适配的全局辅助类

- [x] Task 3: 更新 pages.json 配置
  - [x] 修改 tabBar 配置：backgroundColor #010102，color ink-subtle，selectedColor primary
  - [x] 修改 globalStyle：navigationBarBackgroundColor #010102，navigationBarTextStyle white

- [x] Task 4: 重构登录页 (pages/login.vue)
  - [x] 应用暗黑画布背景、surface-1 输入框、primary 按钮、ink 文字颜色

- [x] Task 5: 重构注册页 (pages/register.vue)
  - [x] 与登录页保持一致的暗黑主题风格

- [x] Task 6: 重构首页 (pages/index.vue)
  - [x] 应用暗黑画布背景，调整 logo 和文字颜色

- [x] Task 7: 重构工作台页面 (pages/work/index.vue)
  - [x] 调整轮播图和宫格组件适配暗黑主题
  - [x] 需要适配 uni-section 组件配色

- [x] Task 8: 重构"我的"页面 (pages/mine/index.vue)
  - [x] 替换蓝色头部为 surface-1 面板，调整所有文字和图标颜色

- [x] Task 9: 重构个人信息页 (pages/mine/info/index.vue)
  - [x] 适配暗黑背景和文字颜色

- [x] Task 10: 重构编辑资料页 (pages/mine/info/edit.vue)
  - [x] 适配表单组件暗黑主题

- [x] Task 11: 重构修改头像页 (pages/mine/avatar/index.vue)
  - [x] 适配暗黑背景

- [x] Task 12: 重构修改密码页 (pages/mine/pwd/index.vue)
  - [x] 适配表单组件暗黑主题

- [x] Task 13: 重构应用设置页 (pages/mine/setting/index.vue)
  - [x] 适配列表和按钮暗黑主题
  - [x] 修复 text-black → text-ink

- [x] Task 14: 重构常见问题页 (pages/mine/help/index.vue)
  - [x] 适配卡片和文字暗黑主题

- [x] Task 15: 重构关于我们页 (pages/mine/about/index.vue)
  - [x] 适配暗黑背景和文字颜色

- [x] Task 16: 重构公共页面 (pages/common/webview + textview)
  - [x] 适配 textview 文字颜色

- [x] Task 17: 更新 uni-section 组件
  - [x] 将组件背景色和文字颜色适配暗黑主题
  - [x] 修复 props 默认颜色值（titleColor: #f7f8f8, subTitleColor: #8a8f98）

# Task Dependencies
- [Task 2] 依赖 [Task 1]（全局样式变量需先定义）
- [Task 4] ~ [Task 17] 均依赖 [Task 1] 和 [Task 2]（页面需引用更新的设计令牌和全局样式）
- [Task 4] ~ [Task 16] 之间彼此独立，可并行执行