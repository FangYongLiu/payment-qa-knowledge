---
id: tbl_kyc_t_compensation_event
object_type: Table
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- infra
- t_compensation_event
subdomain: infra
module: null
sensitivity: normal
name: 补偿事件(t_compensation_event)
aliases:
- t_compensation_event
related_services:
- svc_kyc
related_scenarios: []
---

# 补偿事件(t_compensation_event)

## 用途
**补偿事件表**:失败动作的补偿/重试事件(`execute_status` I/F/S/E,`execute_count` 重试次数,`allow_time` 允许执行时间)。基础设施。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK | 事件id |
| `event_key` | varchar(64) | NOT NULL | 事件主体标志 |
| `main_type` | varchar(32) | NOT NULL | 事件主类型 |
| `sub_type` | varchar(32) | NOT NULL | 事件子类型 |
| `execute_status` | char | NOT NULL | 执行状态: I=初始，F=失败，S=成功，E=异常 |
| `execute_count` | int | NOT NULL | 执行次数 |
| `extension` | varchar(255) |  | 扩展信息 |
| `error_message` | varchar(128) |  | 错误信息 |
| `allow_time` | timestamp |  | 允许执行时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`event_id`)
- 索引 `idx_allow_time`:(`allow_time`)

## 校验点(QA 关注)
- 失败(F/E) 按 allow_time 重试且 execute_count 递增;成功(S) 终止。
- uk(event_key,main_type,sub_type) 幂等。
