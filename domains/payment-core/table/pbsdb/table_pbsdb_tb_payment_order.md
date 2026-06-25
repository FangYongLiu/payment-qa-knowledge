---
id: tbl_pbsdb_tb_payment_order
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
- tb_payment_order
subdomain: pricing
module: null
sensitivity: normal
name: 支付订单表(tb_payment_order)
aliases:
- tb_payment_order
related_services:
- svc_pbs
related_scenarios: []
---
# 支付订单表(tb_payment_order)

## 用途
支付订单表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PAYMENT_ORDER_ID` | decimal(18) | PK / NOT NULL | 支付订单号 |
| `BILL_NO` | decimal(18) |  | 账单号 |
| `PAY_AMOUNT` | decimal(15,2) |  | 支付金额 |
| `PAYER` | varchar(32) |  | 付款方 |
| `PAYEE` | varchar(32) |  | 收款方 |
| `PAYER_ACCOUNT_NO` | varchar(32) |  | 付款方账户 |
| `PAYEE_ACCOUNT_NO` | varchar(32) |  | 收款方账户 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `STATUS` | varchar(20) |  | 1初始状态，2，支付中，3支付成功，4支付失败 |

## 主键 / 索引
- 主键:(`PAYMENT_ORDER_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
