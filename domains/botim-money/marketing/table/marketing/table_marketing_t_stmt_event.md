---
id: tbl_marketing_t_stmt_event
object_type: Table
name: 对账事件 (t_stmt_event)
aliases: [t_stmt_event, marketing.t_stmt_event]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketing schema DDL
tags: [marketing, marketing]
sensitivity: normal
related_services: []
---

# 对账事件 (t_stmt_event)

## 用途
物理表 `marketing.t_stmt_event`,主键 `id`。对账事件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 事件id |
| `transaction_type` | varchar(32) | 事件类型 |
| `stmt_type` | varchar(32) | 对账单类型 |
| `order_type` | varchar(16) | 订单类型 |
| `order_id` | bigint | 账单id |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `i_evt_order`:order_type, order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
