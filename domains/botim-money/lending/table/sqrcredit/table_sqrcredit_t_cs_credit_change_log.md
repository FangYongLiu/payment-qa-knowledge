---
id: tbl_sqrcredit_t_cs_credit_change_log
object_type: Table
name: 额度变更记录 (t_cs_credit_change_log)
aliases: [t_cs_credit_change_log, sqrcredit.t_cs_credit_change_log]
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

# 额度变更记录 (t_cs_credit_change_log)

## 用途
物理表 `sqrcredit.t_cs_credit_change_log`,主键 `id`。额度变更记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(32) | 用户id |
| `amount` | decimal(15, 2) | 金额 |
| `type` | smallint(5) | 类型: 0 增  1 减 |
| `orderNo` | varchar(64) | 订单号 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
