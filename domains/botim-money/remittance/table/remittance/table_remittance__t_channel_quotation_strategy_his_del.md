---
id: tbl_remittance__t_channel_quotation_strategy_his_del
object_type: Table
name: Channel Quotation Strategy History Table (_t_channel_quotation_strategy_his_del)
aliases: [_t_channel_quotation_strategy_his_del, remittance._t_channel_quotation_strategy_his_del]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Channel Quotation Strategy History Table (_t_channel_quotation_strategy_his_del)

## 用途
物理表 `remittance._t_channel_quotation_strategy_his_del`,主键 `id`。Channel Quotation Strategy History Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(20) | Primary Key · 可空 |
| `strategy_id` | int | Strategy ID |
| `channel_code` | varchar(10) | Channel Code |
| `channel_type` | char(6) | Channel Type · 可空 |
| `transaction_mode` | varchar(16) | Remittance Mode |
| `source_currency` | char(3) | Source Currency |
| `target_currency` | char(3) | Target Currency |
| `target_country_code` | char(2) | Target Country (two letters) |
| `target_country_alpha3` | char(3) | Target Country (three letters) · 可空 |
| `bl_amount` | decimal(15, 4) | Base Amount for Exchange Rate · 可空 |
| `exchange_rate` | decimal(15, 8) | Channel Exchange Rate · 可空 |
| `after_mark_rate` | decimal(15, 8) | Exchange Rate after Markup · 可空 |
| `corridor_fee` | decimal(15, 4) | Corridor Fee · 可空 |
| `corridor_fee_currency` | char(3) | Currency for Corridor Fee · 可空 |
| `vat` | decimal(15, 4) | Value Added Tax · 可空 |
| `version` | int(5) | Version Number |
| `change_flag` | char | Rate Change Flag, Y/N · 可空 |
| `buy_rate` | decimal(19, 4) | Purchase Rate · 可空 |
| `operator_name` | varchar(64) | Operator Name · 可空 |
| `operator_time` | timestamp | Operation Time · 可空 |
| `create_time` | timestamp | Creation Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `idx_quotation_strategy_opt`:source_currency, target_currency, target_country_code, create_time
- `idx_sta_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
