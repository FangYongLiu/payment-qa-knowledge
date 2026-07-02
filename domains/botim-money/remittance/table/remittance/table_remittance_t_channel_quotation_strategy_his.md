---
id: tbl_remittance_t_channel_quotation_strategy_his
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_channel_quotation_strategy_his
subdomain: remittance
module: null
sensitivity: normal
name: Channel Quotation Strategy History Table(t_channel_quotation_strategy_his)
aliases:
- t_channel_quotation_strategy_his
related_services:
- svc_remittance
related_scenarios: []
---
# Channel Quotation Strategy History Table(t_channel_quotation_strategy_his)

## 用途
Channel Quotation Strategy History Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(20) | PK / AUTO_INC | Primary Key |
| `strategy_id` | int | NOT NULL | Strategy ID |
| `channel_code` | varchar(10) | NOT NULL | Channel Code |
| `channel_type` | char(6) |  | Channel Type |
| `transaction_mode` | varchar(16) | NOT NULL | Remittance Mode |
| `source_currency` | char(3) | NOT NULL | Source Currency |
| `target_currency` | char(3) | NOT NULL | Target Currency |
| `target_country_code` | char(2) | NOT NULL | Target Country (two letters) |
| `target_country_alpha3` | char(3) |  | Target Country (three letters) |
| `bl_amount` | decimal(15,4) |  | Base Amount for Exchange Rate |
| `exchange_rate` | decimal(15,8) |  | Channel Exchange Rate |
| `after_mark_rate` | decimal(15,8) |  | Exchange Rate after Markup |
| `corridor_fee` | decimal(15,4) |  | Corridor Fee |
| `corridor_fee_currency` | char(3) |  | Currency for Corridor Fee |
| `vat` | decimal(15,4) |  | Value Added Tax |
| `version` | int(5) | NOT NULL / 默认 0 | Version Number |
| `change_flag` | char |  | Rate Change Flag, Y/N |
| `buy_rate` | decimal(19,4) |  | Purchase Rate |
| `operator_name` | varchar(64) |  | Operator Name |
| `operator_time` | timestamp |  | Operation Time |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation Time |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_quotation_strategy_opt` (source_currency, target_currency, target_country_code, create_time)
  - `idx_sta_create_time` (create_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
