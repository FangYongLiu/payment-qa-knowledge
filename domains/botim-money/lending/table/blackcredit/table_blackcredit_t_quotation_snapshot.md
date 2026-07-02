---
id: tbl_blackcredit_t_quotation_snapshot
object_type: Table
name: 汇率报价快照 (t_quotation_snapshot)
aliases: [t_quotation_snapshot, blackcredit.t_quotation_snapshot]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: blackcredit schema DDL
tags: [lending, blackcredit]
sensitivity: normal
related_services: []
---

# 汇率报价快照 (t_quotation_snapshot)

## 用途
物理表 `blackcredit.t_quotation_snapshot`,主键 `id`。汇率报价快照。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `foreign_code` | varchar(8) | 币对代码 |
| `local_code` | varchar(8) | 币对代码 |
| `direction` | varchar(8) | BUY/SELL |
| `rate` | decimal(10, 6) | 汇率 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
