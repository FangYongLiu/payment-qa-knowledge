---
id: tbl_amlreport_tb_eid_limit
object_type: Table
name: eid limit table (tb_eid_limit)
aliases: [tb_eid_limit, amlreport.tb_eid_limit]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# eid limit table (tb_eid_limit)

## 用途
物理表 `amlreport.tb_eid_limit`,主键 `id`。eid limit table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `id_no` | varchar(64) | eid |
| `limit_amount` | decimal(15, 4) | limit amount |
| `currency` | varchar(8) | currency |
| `status` | char | status · 可空 |
| `source` | varchar(20) | source GOOGLE_FORM/AUTO_INCREASE · 可空 |
| `etl_dt` | char(8) | etl date yyyyMMdd · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_etl_dt`:etl_dt
- `idx_id_no`:id_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
