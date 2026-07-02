---
id: tbl_eminstalment_t_notify_event
object_type: Table
name: 记录与电商平台交互的通知事件 (t_notify_event)
aliases: [t_notify_event, eminstalment.t_notify_event]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 记录与电商平台交互的通知事件 (t_notify_event)

## 用途
物理表 `eminstalment.t_notify_event`,主键 `id`。记录与电商平台交互的通知事件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `uniqueId` | varchar(64) | 对应t_goods_order表的orderNo |
| `event_type` | smallint(4) | 事件类型 |
| `event_desc` | varchar(32) | 事件描述 |
| `timestamp` | bigint | 事件发生的时间戳 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |
| `status` | smallint(4) | 待补 |
| `sender` | varchar(16) | 通知生产方 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
