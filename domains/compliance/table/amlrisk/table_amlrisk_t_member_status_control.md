---
id: tbl_amlrisk_t_member_status_control
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_member_status_control
subdomain: amlrisk
module: null
sensitivity: normal
name: member status control(t_member_status_control)
aliases:
- t_member_status_control
related_services:
- svc_aml
related_scenarios: []
---
# member status control(t_member_status_control)

## 用途
member status control。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `member_id` | varchar(20) | NOT NULL | member id |
| `account_no` | varchar(32) |  | basic account no |
| `control_type` | varchar(20) | NOT NULL | control type:MEMBER_OPERATE,ACCOUNT_OPERATE |
| `source` | varchar(20) | NOT NULL | source:Compliance_Auto,Compliance_Manual,Risk_Auto,Risk_Manual |
| `release_flag` | char | NOT NULL / 默认 'N' | N:No,Y:Yes |
| `operate_id` | bigint |  | operate id |
| `release_operate_id` | bigint |  | release operate id |
| `created_time` | timestamp | NOT NULL | Create time |
| `updated_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `ide_updated_time` (updated_time)
  - `idx_account_no` (account_no)
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
