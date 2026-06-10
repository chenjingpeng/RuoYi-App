# 若依移动端 Linear 暗黑主题重设计 Spec

## Why
当前若依移动端所有页面使用白色背景 + 蓝色主题（#007aff / #3c96f3）的浅色模式 UI，与项目根目录 DESIGN.md 定义的 Linear 风格暗黑设计系统不匹配。需要按照 DESIGN.md 规范全面重新生成所有页面样式，应用 Linear 的深色画布 (#010102)、淡紫色品牌强调色 (#5e6ad2)、四阶梯表面系统和自定义字体排版层级。

## What Changes
- 替换 uni.scss 中的全局样式变量为 DESIGN.md 定义的 Linear 设计令牌
- **BREAKING**: 改版 global.scss，移除所有白色背景相关样式，转为暗黑画布体系
- 重新生成 14 个页面的模板与样式，使其符合 Linear 设计规范
- 更新 pages.json 中的 tabBar 和 globalStyle 配置
- 更新 uni-section 组件适配暗黑主题
- 统一所有表单、按钮、卡片、列表等组件为 Linear 风格的对应组件定义

## Impact
- Affected specs: 全局样式系统、所有页面 UI、导航配置
- Affected code:
  - `/workspace/uni.scss` — 设计令牌变量
  - `/workspace/static/scss/global.scss` — 全局辅助样式
  - `/workspace/pages.json` — tabBar / globalStyle 配置
  - `/workspace/components/uni-section/uni-section.vue` — 组件适配
  - `/workspace/pages/*.vue` — 全部 14 个页面文件

## ADDED Requirements

### Requirement: Linear 暗黑设计令牌系统
系统 SHALL 在 uni.scss 中定义完整的 Linear 设计令牌，包括颜色、排版、圆角、间距。

#### Scenario: 全局颜色变量可用
- **WHEN** 开发者在任一页面样式中引用颜色变量
- **THEN** 可以使用 Linear 规范的颜色令牌（如 `$linear-primary: #5e6ad2`, `$linear-canvas: #010102`）

#### Scenario: 全局排版变量可用
- **WHEN** 开发者在任一页面中使用排版变量
- **THEN** 可以使用 Linear 规范的排版令牌（font-size, font-weight, letter-spacing 等）

### Requirement: 暗黑画布 + 表面阶梯系统
系统 SHALL 所有页面默认背景使用 `#010102`（canvas），卡片容器使用表面阶梯递进。

#### Scenario: 页面默认背景
- **WHEN** 打开任意页面
- **THEN** 页面背景为 #010102 深色画布

#### Scenario: 卡片容器在表面层之上
- **WHEN** 页面中存在卡片、面板等容器
- **THEN** 容器背景使用 surface-1 (#0f1011)，带有 hairline (#23252a) 1px 边框

### Requirement: 淡紫色单一品牌强调色
系统 SHALL 仅使用 #5e6ad2 淡紫色作为品牌强调色，用于主 CTA 按钮、链接、输入框焦点环。

#### Scenario: 主按钮样式
- **WHEN** 页面中存在 primary 类型按钮
- **THEN** 按钮背景色为 #5e6ad2，文字白色，圆角 8px，高度符合触摸目标

#### Scenario: 输入框焦点状态
- **WHEN** 输入框获得焦点
- **THEN** 焦点环使用 primary-focus (#5e69d1) 2px outline

### Requirement: 登录/注册页暗黑主题重构
登录和注册页面 SHALL 使用 Linear 暗黑主题风格，表单区域居中显示在深色画布上。

#### Scenario: 登录页样式
- **WHEN** 访问登录页面
- **THEN** 页面背景为深色画布，表单区域居中，输入框使用 surface-1 背景，按钮使用 primary 淡紫色

### Requirement: 首页重构
首页 SHALL 按 Linear 风格重新设计，展示品牌标识和简要介绍。

#### Scenario: 首页展示
- **WHEN** 访问首页
- **THEN** 深色背景上展示品牌 logo 和文字，使用 Linear 排版层级

### Requirement: 工作台页面重构
工作台页面 SHALL 改用 Linear 暗黑风格，轮播图和宫格组件适配暗黑主题。

#### Scenario: 工作台页面展示
- **WHEN** 访问工作台
- **THEN** 页面上所有组件（轮播图、宫格菜单）使用暗黑风格配色

### Requirement: 个人中心/设置页面重构
所有"我的"相关子页面（个人信息、编辑资料、修改密码、应用设置、常见问题、关于我们）SHALL 采用暗黑主题。

#### Scenario: 个人中心页面
- **WHEN** 访问个人中心各子页面
- **THEN** 所有页面背景为深色，卡片/列表使用 surface-1 背景，文字使用 ink/ink-subtle 颜色

### Requirement: 公共页面适配
webview 和 textview 公共页面 SHALL 适配暗黑主题文字颜色。

#### Scenario: 文本展示页
- **WHEN** 访问文本浏览页面
- **THEN** 文字颜色使用 Linear 规范中的 ink/ink-subtle

## MODIFIED Requirements

### Requirement: TabBar 导航配置
TabBar SHALL 使用暗黑配色方案（背景 #010102，选中色 #5e6ad2）。

#### Scenario: TabBar 显示
- **WHEN** 应用加载 TabBar
- **THEN** TabBar 背景为深色，选中项图标/文字为淡紫色，未选中为 ink-subtle

### Requirement: 全局导航栏样式
全局导航栏 SHALL 匹配暗黑主题（背景 #010102，文字白色）。

#### Scenario: 导航栏显示
- **WHEN** 页面加载导航栏
- **THEN** 导航栏背景为深色画布，标题文字为白色