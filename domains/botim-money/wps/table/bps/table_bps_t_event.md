---
id: tbl_bps_t_event
object_type: Table
name: 事件表 (t_event)
aliases: [t_event, bps.t_event]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# 事件表 (t_event)

## 用途
物理表 `bps.t_event`,主键 `id`。事件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `topic` | varchar(128) | 事件主题 |
| `type` | char(16) | 事件类型 |
| `source_id` | varchar(64) | 事件id |
| `data` | varchar(1023) | 事件数据 |
| `status` | char(10) | 事件状态 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
