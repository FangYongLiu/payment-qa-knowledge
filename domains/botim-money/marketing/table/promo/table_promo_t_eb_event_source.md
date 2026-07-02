---
id: tbl_promo_t_eb_event_source
object_type: Table
name: event source entity (t_eb_event_source)
aliases: [t_eb_event_source, promo.t_eb_event_source]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# event source entity (t_eb_event_source)

## 用途
物理表 `promo.t_eb_event_source`,主键 `id`。event source entity。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | char(32) | merchant id |
| `msg_id` | varchar(64) | message id of the event source |
| `msg_app` | varchar(64) | message app of the event source |
| `msg_type` | varchar(64) | message type of the event source |
| `global_track_id` | varchar(64) | global track id of the event source · 可空 |
| `payload` | varchar(1024) | json string of the event payload |
| `status` | varchar(9) | Status: Created|Acked|Processed|Failed|Retried |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |
| `deleted` | tinyint(1) | deleted flag of the event source |

## 主键 / 索引
- 主键:`id`
- `idx_msg_id`:msg_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
