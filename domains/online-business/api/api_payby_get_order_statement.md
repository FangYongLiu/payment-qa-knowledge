---
id: api_payby_get_order_statement
object_type: API
name: 下载对账单 (getOrderStatement)
aliases: [对账单下载, statement-download, getOrderStatement]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: api-docs/payby-api-v2.25-p17 (payby-merchant-api-statement-download)
tags: [online-business, open-api, 对账, 对账单, statement]
related_services: [svc_acquireii, svc_sgs]
related_tables: []
related_scenarios: [scn_online_business_merchant_async_notify]
---

# 下载对账单 (getOrderStatement)

## 用途
商户下载历史对账单,返回 zip 文件流,解压后含 **对账文件 / 结算文件 / 资金文件** 三类 csv,用于核对订单状态、验证结算资金、查看账户资金变动。常用于异步通知缺失或状态不明时的兜底对账(见 [[scn_online_business_merchant_async_notify]])。

三类文件用途:
- **对账文件 (Purchase_Statement)**:所有交易(付款/退款/转账等),核对订单状态、处理掉单/系统错误下的数据不一致。
- **结算文件 (Purchase_Settle_Statement)**:所有已结算付款,含交易与费用明细,核对从 PayBy 收到的资金、预扣费用、退款及调整。
- **资金文件 (fund_statement)**:账户余额收入与支出变化,反映商户账户资金变动。

## 关联关系
- **所属服务**:[[svc_acquireii]](路径在 `/sgs/api/acquire2/...` 下,经 [[svc_sgs]] 网关)(= `related_services`)。
- **读写的表**:待补。
- **被哪些场景测**:[[scn_online_business_merchant_async_notify]](= `related_scenarios`,对账兜底)。

## 路径 / 方法
- 路径:`/sgs/api/acquire2/download/getOrderStatement`
  - 联调:`https://uat.test2pay.com/sgs/api/acquire2/download/getOrderStatement`
  - 生产:`https://api.payby.com/sgs/api/acquire2/download/getOrderStatement`
- 方法:POST

## 入参
**Http Header**

| 参数 | 类型 | 必填 | 示例 | 说明 |
| --- | --- | --- | --- | --- |
| Content-Language | String(10) | N | `en` | 语言 |
| Sign | String | Y | — | 签名(SHA256WithRSA) |
| Partner-Id | String(12) | Y | `200000054800` | 商户号 |

**Http Body**

| 参数 | 类型 | 必填 | 示例 | 说明 |
| --- | --- | --- | --- | --- |
| requestTime | Timestamp(3) | Y | — | 请求时间 |
| bizContent | GetStatementRequest | Y | — | 业务内容,含 `statementDate`(账单日期 `yyyyMMdd`) |

## 出参
- **申请失败**:返回 `application/json`,body 含 `head`(ResponseHeader),如:
  `{ "head": { "applyStatus": "SUCCESS", "code": "62013", "msg": "STATEMENT_NOT_EXIST" } }`
- **申请成功**:文件流返回 zip,关键 Header:
  - `Content-Type: application/zip`
  - `Content-Disposition: attachment; filename=...Transaction_Settle_Statement.zip`

文件名格式:
| 格式 | 示例 |
| --- | --- |
| `PartnerId_dateTransaction_Settle_Statement.zip` | `200000054800_20210112Transaction_Settle_Statement.zip` |
| `Purchase_Statement_date_no.csv` | `Purchase_Statement_13012021_001.csv` |
| `Purchase_Settle_Statement_date_no.csv` | `Purchase_Settle_Statement_13012021_001.csv` |
| `PartnerId_date_fund_statement_no.csv` | `200000054800_20210112_fund_statement_001.csv` |

## 错误码
| code | 含义 | 触发条件 |
| --- | --- | --- |
| 62013 | STATEMENT_NOT_EXIST | 申请的账单日期对账单不存在 |

(其余错误码待补:原文仅给出 62013。)

## 测试校验点(QA)
- **生成时机**:PayBy 在商户设置的结算截止时间立即生成前一天对账单,约 10 分钟内完成;建议商户半小时后再获取(过早请求可能返回 62013)。
- **金额单位**:涉及金额字段单位为迪拉姆 (AED)。
- **未下单订单不入账单**:PayBy 侧未成功下单的订单不出现在对账单;`Purchase_Statement` 不含未完成支付的订单。
- **分文件规则**:单个 csv 不超过 50000 行,超出生成下一编号文件,编号从 `001` 起。
- **文件结构**:
  - `Purchase_Statement`:第 1 行汇总(periodNo/startTime/endTime/totalCount),第 2 行表头,第 3 行起明细(paidTime/transactionType/totalAmount/merchantOrderNo/orderNo/status/payeeMid/terminalId/storeId 等)。
  - `Purchase_Settle_Statement`:汇总含 settlePeriodNo/openingAmount/totalCredit/totalDebit/totalComm(税前手续费)/totalVAT/settleToBank/stayAmount;明细含 settledTime/direction/settlementAmount/comm/VAT 等。
  - `fund_statement`:第 1/2 行汇总(ACCOUNTING_DATE/NUMBER_INCOME 等),第 3 行起明细(原文截断,字段待补)。
- 对账一致性:对账文件订单 ↔ 异步通知 ↔ 查单接口三者状态一致。
