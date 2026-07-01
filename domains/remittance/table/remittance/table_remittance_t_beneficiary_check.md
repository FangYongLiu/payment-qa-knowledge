---
id: tbl_remittance_t_beneficiary_check
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
- t_beneficiary_check
subdomain: remittance
module: null
sensitivity: normal
name: t_beneficiary_check
aliases:
- t_beneficiary_check
related_services:
- svc_remittance
related_scenarios: []
---
# t_beneficiary_check

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | primary key |
| `beneficiary_info_id` | bigint | NOT NULL | beneficiary info id |
| `channel_code` | varchar(32) | NOT NULL | channel code |
| `check_status` | varchar(20) | NOT NULL | check status |
| `create_time` | timestamp | NOT NULL | create time |
| `update_time` | timestamp | NOT NULL | update time |
| `fail_reason` | varchar(128) |  | Fail reason |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_ben_member_id` 唯一 (beneficiary_info_id, channel_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
