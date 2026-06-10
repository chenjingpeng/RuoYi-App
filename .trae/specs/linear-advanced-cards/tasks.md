# Tasks

- [x] Task 1: 修复全局样式和变量
  - [x] 在 uni.scss 中补充第三方组件覆盖所需的 CSS 变量
  - [x] 在 global.scss 中补充 uni-list、uni-easyinput、uni-card 的深色覆盖样式
  - [x] 添加 .btn-primary 统一按钮样式类

- [x] Task 2: 修复设置页选择器错误 (pages/mine/setting/index.vue)
  - [x] 将 `.page` 改为 `page`
  - [x] 为退出登录按钮添加 .btn-primary 样式

- [x] Task 3: 重构首页为高级欢迎页 (pages/index.vue)
  - [x] 添加品牌展示区域（logo + 应用名 + 版本号）
  - [x] 添加快捷入口卡片（surface-1 背景，圆角 12px）
  - [x] 使用 headline 排版层级

- [x] Task 4: 重构工作台宫格图标 (pages/work/index.vue)
  - [x] 为所有 uni-icons 添加 color="#f7f8f8"

- [x] Task 5: 重构"我的"页面卡片化 (pages/mine/index.vue)
  - [x] 头部信息区域改为 surface-1 卡片
  - [x] 快捷操作区改为 surface-1 卡片，图标使用 primary 淡紫色
  - [x] 菜单列表使用 .list-cell 卡片样式

- [x] Task 6: 重构个人信息页 (pages/mine/info/index.vue)
  - [x] 覆盖 uni-list 和 uni-list-item 的浅色背景
  - [x] 为列表添加 surface-1 卡片容器

- [x] Task 7: 重构编辑资料页卡片化 (pages/mine/info/edit.vue)
  - [x] 为表单添加 surface-1 卡片容器包裹
  - [x] 覆盖 uni-easyinput 和 uni-forms 的浅色背景
  - [x] 提交按钮改用 .btn-primary 样式

- [x] Task 8: 重构修改密码页卡片化 (pages/mine/pwd/index.vue)
  - [x] 为表单添加 surface-1 卡片容器包裹
  - [x] 覆盖 uni-easyinput 和 uni-forms 的浅色背景
  - [x] 提交按钮改用 .btn-primary 样式

- [x] Task 9: 重构修改头像页按钮 (pages/mine/avatar/index.vue)
  - [x] 自定义按钮样式替代 type="primary" 和 type="warn"

- [x] Task 10: 重构关于我们页卡片化 (pages/mine/about/index.vue)
  - [x] 信息列表添加 surface-1 卡片容器

- [x] Task 11: 重构常见问题页优化 (pages/mine/help/index.vue)
  - [x] 优化卡片间距和视觉层次

- [x] Task 12: 重构 textview 页卡片化 (pages/common/textview/index.vue)
  - [x] 覆盖 uni-card 浅色背景

# Task Dependencies
- [Task 1] 必须先完成（全局样式和变量是其他任务的基础）
- [Task 2] ~ [Task 12] 彼此独立，可并行执行