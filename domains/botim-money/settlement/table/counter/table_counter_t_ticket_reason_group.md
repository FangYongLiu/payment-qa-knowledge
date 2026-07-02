---
id: tbl_counter_t_ticket_reason_group
object_type: Table
name: 退票原因分组分类表 (t_ticket_reason_group)
aliases: [t_ticket_reason_group, counter.t_ticket_reason_group]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 退票原因分组分类表 (t_ticket_reason_group)

## 用途
物理表 `counter.t_ticket_reason_group`,主键 `id`。退票原因分组分类表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `ticket_code` | varchar(32) | 原因编码 · 可空 |
| `ticket_reason` | varchar(300) | 退票原因 |
| `ticket_class` | varchar(100) | 退票分类 |
| `operator` | varchar(200) | 创建者 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_ticketCode`:ticket_code (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
