---
title: PayBy对账单下载接口
domain: payby-open-api
kind: wiki_page
slug: payby-merchant-api-statement-download
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p17
tags: []
---

# PayBy对账单下载接口

商户通过该接口下载历史对账单，返回 zip 文件流，解压后包含 **对账文件、结算文件、资金文件** 三类 csv，用于核对订单、验证结算资金及查看账户资金变动。

## 应用场景

- **对账文件 (Purchase_Statement)**：包含所有交易（付款、退款、转账等），用于核对订单状态，处理掉单、系统错误等场景下商户与付款方的数据不一致。
- **结算文件 (Purchase_Settle_Statement)**：包含所有已结算的付款，含交易与费用明细，用于核对从 PayBy 收到的资金，了解每笔交易的预扣费用、退款及调整。
- **资金文件 (fund_statement)**：描述账户余额收入与支出变化，反映商户账户资金变动。

## 注意事项

1. PayBy 侧未成功下单的订单不会出现在对账单中。
2. PayBy 在商户设置的结算截止时间立即启动生成前一天的对账单，通常约 10 分钟内完成；建议商户在半小时后再获取。
3. 对账单中涉及金额的字段单位为 **迪拉姆 (AED)**。

## 接口地址

- 联调：`https://uat.test2pay.com/sgs/api/acquire2/download/getOrderStatement`
- 生产：`https://api.payby.com/sgs/api/acquire2/download/getOrderStatement`

详见 [[api_payby_get_order_statement]]。

## 请求参数

**Http Header**

| 字段 | 变量 | 必填 | 类型 |
|---|---|---|---|
| Content-Language | Content-Language | Optional | String(10)，如 `en` |
| Sign | Sign | Required | String |
| Partner-Id | Partner-Id | Required | String(12) |

**Http Body**

| 字段 | 变量 | 必填 | 类型 |
|---|---|---|---|
| 请求时间 | requestTime | Required | Timestamp(3) |
| 业务内容 | bizContent | Required | GetStatementRequest |

`bizContent` 中包含 `statementDate`（账单日期，格式 `yyyyMMdd`）。

## 响应说明

### 申请失败

返回 `application/json`，body 含 `head`（ResponseHeader），如：

```
{ "head": { "applyStatus": "SUCCESS", "code": "62013", "msg": "STATEMENT_NOT_EXIST" } }
```

### 申请成功

以文件流返回 zip 文件，Header 关键字段：

- `Content-Type: application/zip`
- `Content-Disposition: attachment; filename=...Transaction_Settle_Statement.zip`

## 文件名格式

| 文件名格式 | 示例 |
|---|---|
| `PartnerId_dateTransaction_Settle_Statement.zip` | `200000054800_20210112Transaction_Settle_Statement.zip` |
| `Purchase_Statement_date_no.csv` | `Purchase_Statement_13012021_001.csv` |
| `Purchase_Settle_Statement_date_no.csv` | `Purchase_Settle_Statement_13012021_001.csv` |
| `PartnerId_date_fund_statement_no.csv` | `200000054800_20210112_fund_statement_001.csv` |

文件内容规则：

- `Purchase_Statement`：包含所有支付时间在账单日的订单，**不包含未完成支付的订单**。
- `Purchase_Settle_Statement`：包含所有结算时间在账单日的结算订单。
- `fund_statement`：反映商户账户所有的资金变动。
- 单个 csv 文件不超过 50000 行，超出后生成下一个编号文件，编号从 `001` 起始。

## 交易对账文件 (Purchase_Statement)

格式：第 1 行汇总数据，第 2 行表头，第 3 行起为数据。

**汇总字段**：`periodNo`（周期号）、`startTime`（开始时间）、`endTime`（结束时间）、`totalCount`（总记录数）。

**明细字段**：

| 字段 | 说明 |
|---|---|
| paidTime | 支付成功时间 (DD-MM-YYYY HH24:MI:SS) |
| transactionType | 交易类型 |
| totalAmount | 订单金额 |
| orderCurrency | 订单货币 |
| productName | 产品名称 |
| paySceneCode | 支付场景码 |
| merchantOrderNo | 商户订单号 |
| orderNo | PayBy订单号 |
| status | 状态 |
| paymentMethodType | 支付方式 |
| subject | 主题 |
| payeeMid | 收款方会员号 |
| terminalId | 终端编号 |
| operatorId | 操作员编号 |
| storeId | 门店编号 |
| merchantName | 商户名称 |
| storeName | 门店名称 |
| originMerchantOrderNo | 原商户订单号 |
| reserved | 保留字段 |

## 结算对账文件 (Purchase_Settle_Statement)

格式：第 1 行汇总数据，第 2 行表头，第 3 行起为数据。

**汇总字段**：

| 字段 | 说明 |
|---|---|
| settlePeriodNo | 结算周期号 |
| startTime / endTime | 开始/结束时间 |
| openingAmount | 期初金额 |
| totalCount | 总记录数 |
| totalCredit | 总收入 |
| totalDebit | 总支出 |
| totalComm | PayBy 税前手续费汇总 |
| totalVAT | PayBy 增值税汇总 |
| settleToBank | 结算到银行金额及状态 |
| stayAmount | 滞留金额 |

**明细字段**：

| 字段 | 说明 |
|---|---|
| settledTIme | 结算时间 |
| transactionType | 交易类型 |
| direction | 资金方向 |
| settlementAmount | 订单金额 |
| orderCurrency | 订单货币 |
| productName | 产品名称 |
| paySceneCode | 支付场景码 |
| merchantOrderNo | 商户订单号 |
| orderNo | PayBy订单号 |
| paidTime | 支付成功时间 |
| status | 状态 |
| comm | PayBy 税前手续费 |
| commCurrency | 税前手续费货币 |
| VAT | PayBy 增值税 |
| VATCurrency | 增值税货币 |
| paymentMethodType | 支付方式 |
| subject | 主题 |
| payeeMid | 收款方会员号 |
| terminalId | 终端编号 |
| operatorId | 操作员编号 |
| storeId | 门店编号 |
| merchantName | 商户名称 |
| storeName | 门店名称 |
| originMerchantOrderNo | 原商户订单号 |
| reserved | 保留字段 |

## 资金对账文件 (fund_statement)

格式：第 1 行汇总表头，第 2 行汇总数据，第 3 行明细表头，第 4 行起明细数据。

**汇总字段**：

| 字段 | 说明 |
|---|---|
| ACCOUNTING_DATE | 记账日期 |
| NUMBER_INCOME | 收入记录数 |
| AMOU
