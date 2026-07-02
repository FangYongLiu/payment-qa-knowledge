---
id: tbl_pbsdb_tm_bill_config
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
- tm_bill_config
subdomain: pricing
module: null
sensitivity: normal
name: 账单协议表(tm_bill_config)
aliases:
- tm_bill_config
related_services:
- svc_pbs
related_scenarios: []
---
# 账单协议表(tm_bill_config)

## 用途
账单协议表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CONFIG_ID` | decimal(18) | PK / NOT NULL | 商户配置ID |
| `MEMBER_ID` | varchar(32) |  | 商户号 |
| `PARTNER_ID` | varchar(32) |  | 平台方 |
| `BIZ_PRODUCT_CODE` | varchar(20) |  | 业务产品码 |
| `MAX_CREDIT_AMOUNT` | decimal(15,2) |  | 最大赊账金额 |
| `BILL_PERIOD` | varchar(20) |  | M按月，D按天，F每五分钟 |
| `CAL_STRATEGY` | varchar(30) |  | 1消费落地时立即算费，2生成账单时算费 |
| `PAY_STRATEGY` | varchar(30) |  | 1出完账后自动支付，2商户确认后支付 |
| `GMT_NEXT_BILL` | timestamp |  | 下一次结算时间,生成一次账单记录后修改 |
| `PAYER_ACCOUNT_NO` | varchar(50) |  | 付款账户 |
| `PAYER_ACCOUNT_TYPE` | varchar(10) |  | 付款账户类型，BASIC基本户 |
| `STATUS` | varchar(10) |  | 1有效，0失效 |
| `TRIGGER_EXPRESSION` | varchar(50) |  | 为空，表示准时时出账，定时类似cron表达式 |
| `GMT_VALID` | timestamp |  | 生效时间 |
| `GMT_EXPIRE` | timestamp |  | 失效时间 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `PAYEE_ACCOUNT_TYPE` | varchar(10) |  | 收款账户类型 |
| `PAYEE_ACCOUNT_NO` | varchar(50) |  | 收款账户 |
| `VERSION_ID` | decimal(14) | NOT NULL | 乐观锁版本 |

## 主键 / 索引
- 主键:(`CONFIG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
