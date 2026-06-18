---
title: PayBy提现结果页UI说明
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-withdrawal-result-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:950c3db0-ce61-45cb-8e0b-43eafc0af3e7
tags: []
---

# PayBy提现结果页UI说明

提现结果页通过三阶段时间线（Stepper）展示用户从余额提现到银行账户的状态流转，帮助用户了解当前进度及预期到账时间。

## 页面结构

- **页面标题**：Result
- **导航**：左上角返回箭头
- **主体**：垂直时间线，三步骤之间以绿色竖线连接
- **底部 CTA**：整宽绿色按钮 "DONE"（白色大写文字）

## 三阶段状态流

### Step 1 — Transfer request submitted（已完成）

- 状态图标：绿色实心圆 + 白色对勾
- 副文案：Transfer from your balance to your bank account.
- 含义：提现请求已提交，资金从余额转向银行账户

### Step 2 — Your money on its way（已完成）

- 状态图标：绿色实心圆 + 白色对勾
- 副文案：Your bank might take up to 2 working days to complete the transaction.
- 含义：转账在途，银行处理最多需 2 个工作日

### Step 3 — Transfer succeeded（待完成）

- 状态图标：灰色描边圆 + 时钟图标，下方无连接线
- 副文案：If you have any queries, please contact the bank.
- 含义：最终到账成功状态，提交后展示该页时仍处于 pending，等待银行确认

## 状态流转逻辑

请求提交 → 资金在途（≤2 个工作日）→ 转账成功

用户在提交提现后即看到此页面，前两步默认标记为已完成，第三步保持 pending，直到银行确认到账。
