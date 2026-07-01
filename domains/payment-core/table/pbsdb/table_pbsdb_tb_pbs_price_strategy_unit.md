---
id: tbl_pbsdb_tb_pbs_price_strategy_unit
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
- tb_pbs_price_strategy_unit
subdomain: pricing
module: null
sensitivity: normal
name: 新定价策略表(tb_pbs_price_strategy_unit)
aliases:
- tb_pbs_price_strategy_unit
related_services:
- svc_pbs
related_scenarios: []
---
# 新定价策略表(tb_pbs_price_strategy_unit)

## 用途
新定价策略表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PRICE_STRATEGY_ID` | decimal(15) | PK / NOT NULL | 策略ID |
| `NAME` | varchar(50) | NOT NULL | 策略名称 |
| `SCOPE` | char(2) | NOT NULL | 00 - all 01 - payment_code & product_code 02 - payment_code & product_code & billing_memberid 03 - payment_code & product_code & billing_partyrole 04 - payment_code & product_code &  billing_partytype |
| `PRODUCT_CODE` | varchar(32) | NOT NULL | 产品编码 |
| `PAYMENT_CODE` | varchar(32) | NOT NULL | 支付编码 |
| `BILLING_MEMBER_ID` | varchar(64) |  | 会员编码 |
| `BILLING_PARTY_ROLE` | varchar(10) |  | 参与方角色 |
| `BILLING_PARTY_TYPE` | varchar(10) |  | 参与方类型 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `MEMO` | varchar(300) |  | 备注 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `BILLING_PT_ID` | varchar(64) |  | 已废弃 |
| `COMPOSITE_INDEX` | varchar(64) | NOT NULL | 拼接组合索引字段 |

## 主键 / 索引
- 主键:(`PRICE_STRATEGY_ID`)
- 唯一约束:
  - `UK_COMPOSITE_INDEX` 唯一 (COMPOSITE_INDEX)
  - `U_MEMBER_ALL` 唯一 (PRODUCT_CODE, PAYMENT_CODE, SCOPE, BILLING_PARTY_ROLE, BILLING_MEMBER_ID)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
