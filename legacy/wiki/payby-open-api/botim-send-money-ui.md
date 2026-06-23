---
title: Botim Send Money 界面说明
domain: payby-open-api
kind: wiki_page
slug: botim-send-money-ui
status: archived
owner: relink
reviewer: UNREVIEWED
source_type: relink
source_ref: relink:payby-open-api
---

# Botim Send Money 界面说明

本页描述 Botim 应用中"Send money"底部弹窗的 UI 元素与可选转账渠道，用于发起转账操作。相关后端流程参考 [[flow_botim_transfer]]。

## 弹窗整体结构

底部弹窗（bottom sheet）覆盖在聊天页之上，从上到下依次为：
- 标题：`How much do you want to send?`
- 金额输入区
- 快捷金额按钮
- 渠道选择区（`Send money to`）
- 折叠链接（`Show less`）
- 主操作按钮 `Send →`

## 金额输入

- 输入框前缀显示货币符号（迪拉姆字形 `₿`），默认值示例 `1`。
- 快捷金额 chip 按钮一排：`100` / `200` / `500` / `1000`。

## 转账渠道（Send money to）

弹窗列出三种转账方式，用户单选其一，右侧勾选高亮所选项。

### Option 1：botim（默认选中）
- 图标：Botim "b" logo
- 标题：`botim`，附绿色徽标 `🥳 Free`
- 副标题：`Instant to any botim contact.`

### Option 2：Aani
- 图标：Star/Aani logo
- 标题：`Aani`，附绿色徽标 `🥳 Free`
- 副标题：`Instant to any Aani phone number.`
- 价格：`AED 0.5`（带删除线，表示费用已豁免）

### Option 3：International transfer
- 图标：Globe 图标
- 标题：`International transfer`
- 副标题：`Fast at top rates to 150+ countries.`
- 价格：`AED 0`

## 其他控件

- `Show less`：居中蓝色文字链接，用于折叠/展开渠道列表。
- `Send →`：通栏蓝色主 CTA，提交转账。

## 操作流程

用户输入金额 → 选择转账渠道（Botim contact / Aani / International）→ 点击 `Send →` 提交，后端通过 [[api_transfer_place_transfer_order]] 创建转账订单。

## 背景上下文（非弹窗）

弹窗弹出时，背景聊天页被置灰，其内容包括：
- 聊天头部：返回箭头、头像 `夏`、联系人 `夏一冰`、副标题 `Last seen: Yesterday at 19:53`、视频与语音通话图标。
- 一条交易卡片：金额 `AED 125.00`，绿色勾选状态 `Transferred - Oct 12`，右侧 chevron。
