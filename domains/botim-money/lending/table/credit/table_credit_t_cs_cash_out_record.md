---
id: tbl_credit_t_cs_cash_out_record
object_type: Table
name: Citi account withdrawal record (t_cs_cash_out_record)
aliases: [t_cs_cash_out_record, credit.t_cs_cash_out_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# Citi account withdrawal record (t_cs_cash_out_record)

## 用途
物理表 `credit.t_cs_cash_out_record`,主键 `id`。Citi account withdrawal record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `created_time` | timestamp | create time |
| `last_modified` | timestamp | update time |
| `status` | tinyint(5) | -1:fail , 0:init , 1:wait , 2:success |
| `type` | tinyint(5) | 1:buyback |
| `payment_account` | varchar(30) | payment account |
| `receive_account` | varchar(30) | receive account |
| `amount` | decimal(15, 2) | amount |
| `payment_time` | timestamp | payment time · 可空 |
| `payment_no` | bigint | payment no 13**************** · 可空 |
| `settle_time` | timestamp | settle success event time · 可空 |
| `capital` | decimal(15, 2) | capital |
| `interest` | decimal(15, 2) | interest |
| `penalty` | decimal(15, 2) | penalty |
| `extension_fee` | decimal(15, 2) | extension_fee |
| `early_settlement_fee` | decimal(15, 2) | early_settlement_fee |
| `channel_fee` | decimal(15, 2) | channel_fee |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
