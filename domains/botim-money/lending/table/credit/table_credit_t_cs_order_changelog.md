---
id: tbl_credit_t_cs_order_changelog
object_type: Table
name: 订单状态记录 (t_cs_order_changelog)
aliases: [t_cs_order_changelog, credit.t_cs_order_changelog]
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

# 订单状态记录 (t_cs_order_changelog)

## 用途
物理表 `credit.t_cs_order_changelog`,主键 `id`。订单状态记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主键 · 可空 |
| `pre_status` | smallint(5) | 前状态 |
| `after_status` | smallint(5) | 后状态 |
| `operator` | varchar(50) | 操作人 |
| `order_no` | varchar(64) | 订单号 |
| `created_time` | timestamp | 待补 · 可空 |
| `updated_time` | timestamp | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
