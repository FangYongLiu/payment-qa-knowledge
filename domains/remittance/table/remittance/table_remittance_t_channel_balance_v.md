---
id: tbl_remittance_t_channel_balance_v
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_channel_balance_v
subdomain: remittance
module: null
sensitivity: normal
name: Channel balance(t_channel_balance_v)
aliases:
- t_channel_balance_v
related_services:
- svc_remittance
related_scenarios: []
---
# Channel balance(t_channel_balance_v)

## 用途
Channel balance。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key |
| `channel_code` | varchar(12) | NOT NULL | Channel code |
| `country_code` | char(2) | NOT NULL | Country code |
| `amount` | decimal(18,4) |  | Available amount |
| `currency` | varchar(32) |  | Currency |
| `org_amount` | decimal(18,6) |  | Original amount from channel |
| `org_currency` | varchar(10) |  | Original currency from channel |
| `sync_time` | timestamp | NOT NULL | Balance sync time |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |
| `operator` | varchar(30) | NOT NULL / 默认 'system' | operator name |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
