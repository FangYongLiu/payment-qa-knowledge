---
title: Botim转账成功确认页面UI说明
domain: fund-out-transfer
kind: wiki_page
slug: botim-transfer-success-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:26a4f98a-7c49-4353-986b-7c481f2e8fff
tags: []
---

# Botim转账成功确认页面UI说明

本页描述 Botim 聊天内点对点转账成功后弹出的确认弹窗 UI 元素，以及聊天会话中转账历史记录的展示形式。

## 页面入口与场景

- 用户在 Botim 聊天会话中发起点对点转账，转账成功后由系统弹出底部 bottom sheet 模态框。
- 用户点击确认后返回聊天会话，新转账记录会与历史 "Transferred" 记录一同显示在聊天流中。

## 成功确认弹窗（前景 Bottom Sheet）

弹窗为底部抬起的模态层，包含以下元素：

- **图标**：大尺寸绿色 3D 硬币/徽章图样，中心带勾选标记（checkmark）。
- **标题**：加粗大字 "Successful transaction!"。
- **字段行**（浅灰色胶囊容器）：
  - 左侧 label：`Transaction ID`
  - 右侧 value：交易号（示例 "311760..."，长号展示）
- **主操作按钮**：全宽、蓝色、圆角 CTA 按钮，文案 "Okay"，点击后关闭弹窗。
- 底部为 iOS home indicator 指示条。

## 聊天背景中的转账历史展示

弹窗弹出时，背景为该联系人聊天会话页面（处于 dim 暗化状态）：

### 顶部 Header

- 左侧：返回箭头、联系人头像与昵称
- 副标题：联系人在线状态，如 `Last seen: Yesterday at 19:53`
- 右侧：视频通话、语音通话图标

### 转账记录卡片

聊天流中按日期分组展示多条转账 receipt 卡片，每条卡片包含：

- 绿色 checkmark 图标
- 金额行：如 `AED 80.00`、`AED 100.00`
- 状态行：`Transferred - Oct 14` / `Transferred - Oct 16` / `Transferred - Oct 19`，行尾带右向 chevron `>`（可点击查看详情）
- 副文案：`Botim transfer` + 发送时间戳（如 `8:34`、`22:45`、`11:57`）

### 日期分组

聊天流中以日期分隔符区分，例如 `Thursday`、`Yesterday`。

## 交互流转

- 弹窗仅提供单一操作 `Okay`，无其他分支动作。
- 关闭弹窗后用户回到聊天会话，新生成的转账 receipt 卡片会追加到历史记录列表末尾。
