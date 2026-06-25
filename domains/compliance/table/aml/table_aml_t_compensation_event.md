---
id: tbl_aml_t_compensation_event
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_compensation_event
subdomain: aml
module: null
sensitivity: normal
name: 补偿事件(t_compensation_event)
aliases:
- t_compensation_event
related_services:
- svc_aml
related_scenarios: []
---
# 补偿事件(t_compensation_event)

## 用途
补偿事件。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK / AUTO_INC | 事件id |
| `event_key` | varchar(64) | NOT NULL | 事件主体标志 |
| `main_type` | varchar(32) | NOT NULL | 事件主类型 |
| `sub_type` | varchar(32) | NOT NULL | 事件子类型 |
| `execute_status` | char | NOT NULL | 执行状态：I=初始，F=失败，S=成功，E=异常 |
| `execute_count` | int | NOT NULL | 执行次数 |
| `extension` | varchar(255) |  | 扩展信息 |
| `error_message` | varchar(128) |  | 错误信息 |
| `allow_time` | timestamp |  | 允许执行时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`event_id`)
- 唯一约束:
  - `uk_event_key_type_subtype` 唯一 (event_key, main_type, sub_type)
- 索引:
  - `idx_allow_time` (allow_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
