---
title: PayBy提现结果页UI说明
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-withdrawal-result-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:11dc7a69-8bfe-4b75-ad06-28c0d98e8fd3
tags: []
---

# PayBy提现结果页UI说明

提现结果页（Result）以三步状态时间线展示提现进度，包含成功节点与失败节点的提示文案，并在底部提供操作按钮。

## 页面基础结构

- 页面标题：**Result**
- 左上角返回按钮：`<`
- 主体：垂直 3 步状态时间线，节点之间用绿色竖线连接
- 底部：全宽绿色按钮 **DONE**（白色大写文字）

## 三步状态时间线

### Step 1 — Transfer request approved
- 图标：绿色对勾（成功）
- 标题：Transfer request approved
- 副标题：Transfer from your balance to your bank account.

### Step 2 — Your money on its way
- 图标：绿色对勾（成功）
- 标题：Your money on its way
- 副标题：Your bank might take up to 2 working days to complete the transaction.

### Step 3 — Transfer failed
- 图标：红色圆底白色 X（失败）
- 标题：Transfer failed
- 副标题：You will receive a refund. Please contact help@payby.com for more details.

## 失败场景说明

当提现流程在最终转账环节失败时：

- 前两步（请求已批准、资金在途）展示为成功状态
- 第三步展示为失败状态
- 用户将收到退款（refund）
- 提示用户联系 **help@payby.com** 获取更多详情
