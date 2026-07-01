---
id: tbl_merchant_t_compensation_event
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_compensation_event
subdomain: merchant
module: null
sensitivity: normal
name: compensation event(t_compensation_event)
aliases:
- t_compensation_event
related_services:
- svc_merchant
related_scenarios: []
---
# compensation event(t_compensation_event)

## 用途
compensation event。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK / AUTO_INC | event id |
| `event_key` | varchar(64) | NOT NULL | event key |
| `main_type` | varchar(32) | NOT NULL | main type |
| `sub_type` | varchar(32) | NOT NULL | sub type |
| `execute_status` | char | NOT NULL | execute status: I，F，S，E |
| `execute_count` | int | NOT NULL | execute count |
| `extension` | varchar(255) |  | extension |
| `error_message` | varchar(128) |  | error message |
| `allow_time` | timestamp |  | allow time |
| `create_time` | timestamp | NOT NULL | create time |
| `update_time` | timestamp | NOT NULL | update time |

## 主键 / 索引
- 主键:(`event_id`)
- 唯一约束:
  - `uk_event_key_type_subtype` 唯一 (event_key, main_type, sub_type)
- 索引:
  - `idx_allow_time` (allow_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
