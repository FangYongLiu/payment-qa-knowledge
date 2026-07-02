---
id: tbl_invoice_t_invoice_history
object_type: Table
name: es同步任务 (t_invoice_history)
aliases: [t_invoice_history, invoice.t_invoice_history]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: invoice schema DDL
tags: [merchant-management, invoice]
sensitivity: normal
related_services: []
---

# es同步任务 (t_invoice_history)

## 用途
物理表 `invoice.t_invoice_history`,主键 `id`。es同步任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `invoice_order_id` | bigint | 关联订单 |
| `content` | varchar(200) | 内容 |
| `remark` | varchar(200) | 备注 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `operator_name` | varchar(255) | operator_name · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_history_iid`:invoice_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
