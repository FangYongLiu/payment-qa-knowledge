---
id: tbl_escrowii_t_compensation_event
object_type: Table
name: Compensation event (t_compensation_event)
aliases: [t_compensation_event, escrowii.t_compensation_event]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrowii schema DDL
tags: [deposit-vam, escrowii]
sensitivity: normal
related_services: []
---

# Compensation event (t_compensation_event)

## 用途
物理表 `escrowii.t_compensation_event`,主键 `event_id`。Compensation event。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_id` | bigint | event id · 可空 |
| `event_key` | varchar(64) | event main key |
| `main_type` | varchar(32) | main type |
| `sub_type` | varchar(32) | sub type |
| `execute_status` | char | Execute status: I=Initial，F=Fail，S=Success，E=Error |
| `execute_count` | int | Execute count |
| `extension` | varchar(255) | Extension info · 可空 |
| `error_message` | varchar(128) | error msg · 可空 |
| `allow_time` | timestamp | allow time · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | modify time |

## 主键 / 索引
- 主键:`event_id`
- `uk_event_key_type_subtype`:event_key, main_type, sub_type (UNIQUE)
- `idx_allow_time`:allow_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
