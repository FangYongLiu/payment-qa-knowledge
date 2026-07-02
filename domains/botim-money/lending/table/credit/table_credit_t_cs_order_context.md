---
id: tbl_credit_t_cs_order_context
object_type: Table
name: 订单上下文 (t_cs_order_context)
aliases: [t_cs_order_context, credit.t_cs_order_context]
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

# 订单上下文 (t_cs_order_context)

## 用途
物理表 `credit.t_cs_order_context`,主键 `id`。订单上下文。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主键 · 可空 |
| `order_no` | varchar(64) | order no, UUID |
| `device_snap` | varchar(7000) | user device snapshot · 可空 |
| `profile_snap` | varchar(3000) | user profile snapshot · 可空 |
| `channel` | varchar(50) | 渠道 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |
| `disbursement_snap` | varchar(1024) | disbursement card snapshot · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
