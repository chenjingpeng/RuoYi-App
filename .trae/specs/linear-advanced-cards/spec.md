# Linear 暗黑主题高级卡片化重构 Spec

## Why
当前页面虽已应用暗黑底色，但存在以下问题：
1. 第三方组件（uni-list、uni-easyinput、uni-card）可能透出白色/浅色背景，与暗黑主题割裂
2. 表单页（编辑资料、修改密码）直接平铺，无卡片容器包裹，视觉层次单薄
3. 首页过于简单，仅有 logo 和文字
4. 工作台宫格图标未指定颜色，在暗黑背景下可能不可见
5. 设置页 `.page` 选择器错误导致背景样式不生效
6. "我的"页面需要更精致的卡片化设计，提升高级感

## What Changes
- 修复所有第三方组件的浅色背景透出（uni-list、uni-easyinput、uni-card）
- 表单页增加 surface-1 卡片容器包裹，提升视觉层次
- 首页重新设计为高级欢迎页，包含品牌卡片和快捷入口
- 工作台宫格图标统一指定 ink 颜色
- 修复设置页选择器错误
- "我的"页面全面卡片化：头部信息卡片、快捷操作卡片、菜单列表卡片
- 所有按钮统一使用 primary 淡紫色主题

## Impact
- Affected code: 全部 14 个页面文件 + uni.scss 补充变量 + global.scss 补充样式

## ADDED Requirements

### Requirement: 第三方组件浅色背景修复
系统 SHALL 通过 CSS 深度选择器覆盖所有第三方组件的默认浅色背景。

#### Scenario: uni-list 组件
- **WHEN** 页面使用 uni-list 展示信息
- **THEN** 列表项背景为 surface-1 (#0f1011)，文字为 ink (#f7f8f8)

#### Scenario: uni-easyinput 组件
- **WHEN** 表单使用 uni-easyinput 输入框
- **THEN** 输入框背景为 surface-1，边框为 hairline，文字为 ink

#### Scenario: uni-card 组件
- **WHEN** 页面使用 uni-card 卡片
- **THEN** 卡片背景为 surface-1，边框为 hairline

### Requirement: 表单页卡片化
编辑资料页和修改密码页 SHALL 使用 surface-1 卡片容器包裹表单内容。

#### Scenario: 编辑资料页
- **WHEN** 访问编辑资料页
- **THEN** 表单区域被 surface-1 卡片包裹，圆角 12px，带 hairline 边框

#### Scenario: 修改密码页
- **WHEN** 访问修改密码页
- **THEN** 表单区域被 surface-1 卡片包裹，提交按钮使用 primary 淡紫色

### Requirement: 首页高级化重构
首页 SHALL 重新设计为包含品牌展示、版本信息、快捷入口的高级欢迎页。

#### Scenario: 首页展示
- **WHEN** 访问首页
- **THEN** 看到品牌 logo、应用名称、版本号，以及 surface-1 卡片包裹的快捷入口

### Requirement: 工作台宫格图标适配
工作台页面的 uni-icons SHALL 统一指定颜色。

#### Scenario: 宫格图标显示
- **WHEN** 访问工作台
- **THEN** 所有宫格图标颜色为 ink (#f7f8f8) 或 ink-muted (#d0d6e0)

### Requirement: "我的"页面全面卡片化
"我的"页面 SHALL 使用卡片化设计：头部信息卡片、快捷操作卡片、菜单列表卡片。

#### Scenario: 个人中心展示
- **WHEN** 访问"我的"页面
- **THEN** 头部使用 surface-1 卡片展示用户信息，快捷操作区使用卡片，菜单列表使用卡片

### Requirement: 设置页修复
设置页 SHALL 修复选择器错误，并统一按钮样式。

#### Scenario: 设置页显示
- **WHEN** 访问设置页
- **THEN** 页面背景正确生效，退出登录按钮使用 primary 淡紫色

### Requirement: 按钮统一主题
所有原生 button SHALL 使用自定义样式替代默认 type="primary"。

#### Scenario: 提交按钮
- **WHEN** 页面存在提交按钮
- **THEN** 按钮背景为 #5e6ad2，文字白色，圆角 8px
