---
id: api_payby_get_order_statement
object_type: API
domain: payby-open-api
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p17
tags:
- 对账单
- 下载
- statement
- zip
subdomain: statement
module: download
sensitivity: normal
name: 下载对账单接口 (getOrderStatement)
aliases:
- getOrderStatement
related_services: []
related_tables: []
related_scenarios:
- payby-merchant-api-statement-download
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
商户按账单日期下载历史对账单，返回zip文件，内含3个csv：
- 对账文件 (Purchase_Statement)：所有交易（支付、退款、转账等），用于核对订单状态、修正掉单/系统错误导致的数据不一致。
- 结算文件 (Purchase_Settle_Statement)：所有已结算的付款及费用明细，用于核对从PayBy收到的资金、退款、调整、预扣费用。
- 资金文件 (fund_statement)：账户余额收支变化，反映商户账户资金变动。

注意：
1. PayBy侧未成功下单的订单不会出现在对账单中。
2. PayBy 在结算截止时间立即生成前一天对账单，约 10 分钟生成完毕，建议商户半小时后再获取。
3. 对账单金额字段单位为"迪拉姆"。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/download/getOrderStatement
- 生产URL: https://api.payby.com/sgs/api/acquire2/download/getOrderStatement
- 方法：HTTP POST，Content-Type: application/json

## 入参
Http Header：
- Content-Language（Optional, String(10)）：文案语言，如 `en`
- Sign（Required, String）：签名
- Partner-Id（Required, String(12)）：商户号

Http Body：
- requestTime（Required, Timestamp(3)）：请求时间，如 `1581493898000`
- bizContent（Required, GetStatementRequest）：业务内容
  - statementDate：账单日期（示例 `20200605`）

请求样例 body：
```json
{
  "body": {
    "bizContent": { "statementDate": "20200605" },
    "requestTime": 1585142880000
  }
}
```

## 出参

### 申请失败（JSON）
Http Header：
- Content-Language（Optional, String(10)）
- Sign（Required, String）
- Partner-Id（Required, String(12)）
- Content-Type（Required, String(256)）：`application/json`

Http Body：
- head（Required, ResponseHeader）：包含 applyStatus、code、msg、traceCode

样例：
```json
{
  "head": {
    "applyStatus": "SUCCESS",
    "code": "62013",
    "msg": "STATEMENT_NOT_EXIST",
    "traceCode": "1133"
  }
}
```

### 申请成功（文件流）
Http Header：
- Content-Disposition（Required, String）：如 `attachment; filename=200000054800_20210112Transaction_Settle_Statement.zip`
- Content-Type（Required, String）：`application/zip`

数据以文件流返回 .zip，解压得到 csv。

文件名格式：
| 文件名格式 | 文件名示例 |
|---|---|
| PartnerId_dateTransaction_Settle_Statement.zip | 200000054800_20210112Transaction_Settle_Statement.zip |
| Purchase_Statement_date_no.csv | Purchase_Statement_13012021_001.csv |
| Purchase_Settle_Statement_date_no.csv | Purchase_Settle_Statement_13012021_001.csv |
| PartnerId_date_fund_statement_no.csv | 200000054800_20210112_fund_statement_001.csv |

说明：
1. Purchase_Statement：支付时间在账单日的所有订单（不含未完成支付）。
2. Purchase_Settle_Statement：结算时间在账单日的所有结算订单。
3. fund_statement：商户账户的所有资金变动。
4. 单 csv 不超过 50000 行，超过则按 001、002… 编号分文件。

#### 交易对账文件 (Purchase_Statement)
- 第1行：汇总（periodNo、startTime、endTime、totalCount）
- 第2行：表头
- 第3行起：明细

明细字段：paidTime、transactionType、totalAmount、orderCurrency、productName、paySceneCode、merchantOrderNo、orderNo、status、paymentMethodType、subject、payeeMid、terminalId、operatorId、storeId、merchantName、storeName、originMerchantOrderNo、reserved。

#### 结算对账文件 (Purchase_Settle_Statement)
- 第1行汇总：settlePeriodNo、startTime、endTime、openingAmount、totalCount、totalCredit、totalDebit、totalComm（PayBy税前手续费汇总）、totalVAT（PayBy增值税汇总）、settleToBank（结算到银行金额及状态）、stayAmount（滞留金额）
- 第2行表头，第3行起明细

明细字段：settledTIme、transactionType、direction、settlementAmount、orderCurrency、productName、paySceneCode、merchantOrderNo、orderNo、paidTime、status、comm、commCurrency、VAT、VATCurrency、paymentMethodType、subject、payeeMid、terminalId、operatorId、storeId、merchantName、storeName、originMerchantOrderNo、reserved。

#### 资金对账文件 (fund_statement)
- 第1行：汇总表头（ACCOUNTING_DATE、NUMBER_INCOME、AMOUNT_INCOME、NUMBER_PAYOUT、AMOUNT_PAYOUT、BEGINNING_BALANCE、ENDING_BALANCE）
- 第2行：汇总数据
- 第3行：明细表头
- 第4行起：明细

明细字段：ACCOUNTING_TIME、TXN_NO、PRODUCT、BUSINESS_TYPE、DIRECTION、TXN_AMT、BEFORE_AMT、AFTER_AMT、ACCOUNT_TYPE、MERCHANT_ORDER_NO、ORDER_NO。

## 错误码
| code | msg | 原因 | 解决方案 |
|---|---|---|---|
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重
