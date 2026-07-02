---
id: tbl_sqrcredit_t_cs_black_credit
object_type: Table
name: 总授信 (t_cs_black_credit)
aliases: [t_cs_black_credit, sqrcredit.t_cs_black_credit]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sqrcredit schema DDL
tags: [lending, sqrcredit]
sensitivity: normal
related_services: []
---

# 总授信 (t_cs_black_credit)

## 用途
物理表 `sqrcredit.t_cs_black_credit`,主键 `id`。总授信。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `total_amount` | decimal(15, 2) | 总金额 |
| `used_total_amount` | decimal(15, 2) | 已授权金额 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
