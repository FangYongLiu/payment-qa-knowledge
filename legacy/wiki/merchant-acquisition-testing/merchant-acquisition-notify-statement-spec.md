---
title: 异步通知与对账文件结构
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-notify-statement-spec
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 异步通知与对账文件结构

商户收单的"最后一公里"——异步通知（notifyUrl）与 T+1 对账单——是 [[merchant-acquisition-e2e-five-stage-verification]] 中段⑤的核心校验内容。本页定义重试策略、商户应答规范、对账单 ZIP 结构与 CSV 关键字段。

## 异步通知 notifyUrl

### 重试策略

最多 7 次，累计约 24 小时窗口；失败则按下表间隔重试：

```
首次       → 失败
2 分钟后   → 第 2 次
+10 分钟   → 第 3 次
+10 分钟   → 第 4 次
+60 分钟   → 第 5 次
+120 分钟  → 第 6 次
+360 分钟  → 第 7 次
+900 分钟  → 放弃（不再重试）
```

> Botim 不保证最终送达，因此商户需"通知 + 主动查询"双保险。

### 通知 body 关键字段

- `notify_id`（唯一）
- `notify_timestamp`
- 订单对象（`acquireOrder` / `refundOrder` 等）

### 商户响应规范

任一不满足即视为失败、触发重试：

- HTTP 状态：`200`
- `Content-Type: application/json`
- Body：`{"response": "SUCCESS"}`

### 测试要点

- 验证 body 字段完整
- 故意返回非 SUCCESS / 非 200 / 超时 → 验证重试时间表（2 → 10 → 10 → 60 → 120 → 360 → 900）
- 验证第 7 次后停止重试
- 模拟工具：webhook.site、ngrok / frp、内部回调测试服务（详见 [[merchant-acquisition-test-data-preparation]]）

## 对账单结构

商户调用 `/sgs/api/acquire2/download/getOrderStatement` 获取 ZIP。

### ZIP 文件结构

```
PartnerId_dateTransaction_Settle_Statement.zip
├── Purchase_Statement_date_no.csv         （Transaction Statement，交易明细）
├── Purchase_Settle_Statement_date_no.csv  （Settlement Statement，结算明细）
└── PartnerId_date_fund_statement_no.csv   （Fund Statement，资金流水）
```

### 关键约束

- 每个 CSV 最多 **50,000 行**，超出按 `001`、`002` 编号分片
- **未支付订单不进对账单**
- T+1 上午约 10 分钟生成，建议 **30 分钟后下载**
- ⭐ **PreAuth 不进对账单，Capture 才进**

## CSV 关键字段

### Transaction Statement

`transactionType` 共 13 种枚举：

`PAYMENT` / `REFUND` / `VOID` / `DEPOSIT` / `TRANSFER` / `EATM` / `ADJUST` / `KIOSK` / `WITHDRAWAL` / `REFUND_SPLIT` / `PAYMENT_SPLIT` / `CHARGE` / `CHARGEBACK`

`status`：

- `SUCCESS`
- `REVERTED`（**Revoke 在这里显示为 REVERTED**）

### Settlement Statement

- `direction`：`CREDIT`（入款） / `DEBIT`（出款）
- `comm`：税前佣金
- `VAT`：税额

Settlement 等式：

```
totalCredit - totalDebit = settleToBank + stayAmount
```

## 对账测试要点

- 跨日订单的归属（23:59 创建、0:01 通知 → 算哪一天的对账单）
- Revoke 显示为 `REVERTED`，Refund 显示为 `REFUND`，不要混淆
- Settlement 等式两端必须对平
- PreAuth 单独验证"不在对账单中"，Capture 后再次验证"已进对账单"

> 下载接口的 curl 调用模板见 [[merchant-acquisition-curl-postman-templates]]；逐笔交易的对账核对项见 [[merchant-acquisition-per-transaction-checklist]]。
