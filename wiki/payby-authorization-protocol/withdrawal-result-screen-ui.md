---
title: 提现结果页UI说明
domain: payby-authorization-protocol
kind: wiki_page
slug: withdrawal-result-screen-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:087407ec-1565-4ba3-b668-cc4a079a7890
tags: []
---

# 提现结果页UI说明

提现申请提交后展示的结果页，使用三步进度指示器告知用户当前提现状态及预期到账时间。

## 页面标题

- 标题：**Result**

## 三步进度指示器

页面主体为竖向三步进度时间轴，左侧图标通过竖线连接，每步包含加粗标题与灰色副标题。

### Step 1（已完成）

- 状态图标：绿色实心圆 + 白色对勾，下方连接线为绿色
- 标题：**Transfer request approved**
- 副标题：Transfer from your balance to your bank account.

### Step 2（待完成）

- 状态图标：空心圆 + 时钟图标，下方连接线为灰色
- 标题：**Your money on its way**
- 副标题：Your bank might take up to 2 working days to complete the transaction.

### Step 3（待完成）

- 状态图标：空心圆 + 时钟图标
- 标题：**Transfer succeeded**
- 副标题：If you have any queries, please contact the bank.

## 底部按钮与链接

- 主按钮：绿色背景、白色大写文字 **DONE**，点击关闭/返回
- 文字链接：**History >**（带右向箭头），跳转查看历史交易记录

## 业务含义

- 表示提现申请已被受理并进入处理流程
- 当前仅完成第一步，资金正在转往用户银行账户途中
- 银行处理 SLA：最长 2 个工作日
