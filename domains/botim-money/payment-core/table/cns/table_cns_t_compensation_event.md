---
id: tbl_cns_t_compensation_event
object_type: Table
name: Compensation Event (t_compensation_event)
aliases: [t_compensation_event, cns.t_compensation_event]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cns schema DDL
tags: [payment-core, cns]
sensitivity: normal
related_services: []
---

# Compensation Event (t_compensation_event)

## 用途
物理表 `cns.t_compensation_event`,主键 `event_id`。Compensation Event。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_id` | bigint | Event id · 可空 |
| `event_key` | varchar(64) | Event key |
| `main_type` | varchar(32) | Main type |
| `sub_type` | varchar(32) | Sub type |
| `execute_status` | char | I=Init, F=Fail, S=Success, E=Error |
| `execute_count` | int | Execute count |
| `extension` | varchar(512) | Extension · 可空 |
| `error_message` | varchar(128) | Error message · 可空 |
| `allow_time` | timestamp | Allow execute time · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`event_id`
- `uk_event_key_type_subtype`:event_key, main_type, sub_type (UNIQUE)
- `idx_allow_time`:allow_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
