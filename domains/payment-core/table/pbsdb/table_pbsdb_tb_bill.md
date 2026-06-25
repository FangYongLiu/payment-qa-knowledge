---
id: tbl_pbsdb_tb_bill
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_bill
subdomain: pricing
module: null
sensitivity: normal
name: 账单表(tb_bill)
aliases:
- tb_bill
related_services:
- svc_pbs
related_scenarios: []
---
# 账单表(tb_bill)

## 用途
账单表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BILL_NO` | decimal(18) | PK / NOT NULL | 账单号 |
| `TRADE_COUNT` | decimal(15) |  | 交易次数 |
| `MEMBER_ID` | varchar(32) |  | 商户号 |
| `PARTNER_ID` | varchar(32) |  | 平台方 |
| `BIZ_PRODUCT_CODE` | varchar(20) |  | 业务产品码 |
| `BILL_AMOUNT` | decimal(15,2) |  | 账单金额 |
| `GMT_PAY` | timestamp |  | 最后支付时间 |
| `STATUS` | varchar(10) |  | 1初始状态，2算费失败，3待支付，4支付失败，5已支付 |
| `ERROR_MSG` | varchar(30) |  | 账单支付失败原因 |
| `GMT_RETRY` | timestamp |  | 下次重试时间 |
| `RETRY_TIMES` | decimal(3) |  | 重试次数 |
| `BILL_TYPE` | varchar(10) |  | 1自动账单，2手动账单 |
| `GMT_BILL_START` | timestamp |  | 账单起始时间 |
| `GMT_BILL_FINISH` | timestamp |  | 账单结束时间 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`BILL_NO`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
