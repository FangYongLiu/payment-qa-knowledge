---
title: PayBy提现通知界面说明
domain: authorization-protocol
kind: wiki_page
slug: payby-withdrawal-notification-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:f301f96b-3d22-4409-956f-fa4f54effd7f
tags: []
---

# PayBy提现通知界面说明

本页说明 PayBy App 内"提现到银行卡"通知消息卡片的界面构成与展示字段，便于核对提现交易的关键信息与跳转入口。

## 页面定位与导航

- 入口：App 内 PayBy 聊天式通知页面（顶部标题为 **PayBy**，左侧返回箭头，配 PayBy 绿色圆形 Logo）
- 通知按时间分组展示，顶部居中显示日期分隔标签（如 `Today`）
- 背景为绿色购物图标花纹（购物袋、购物车、标签、卡片等）

## 通知卡片字段

提现通知以白色卡片形式展示，字段如下：

- **标题**：`Transfer to Your Bank`
- **金额**：大号加粗显示，例 `AED 1.00`
- **Status**：交易状态，例 `Processing`
- **Order No.**：订单号，例 `131602480114014699`
- **Time**：交易时间，格式 `DD-MM-YYYY HH:mm`，例 `12-10-2020 13:21`
- 分隔线下方为 `View Detail` 链接，附右向箭头（>），点击进入提现详情页

## 状态语义

- `Processing`：表示该笔银行卡提现已发起，正在处理中

## 底部输入栏

通知页底部为聊天输入栏（仅作为页面布局组件，不参与提现业务）：

- 左侧绿色 `+` 图标
- 中间 `Message` 占位文本输入框，含表情图标
- 右侧绿色圆形发送按钮（白色箭头）

## 示例数据快照

| 字段 | 值 |
|---|---|
| Transfer to | Your Bank |
| Amount | AED 1.00 |
| Status | Processing |
| Order No. | 131602480114014699 |
| Time | 12-10-2020 13:21 |
