---
id: tbl_amlrisk_t_member_status_operate
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
- t_member_status_operate
subdomain: amlrisk
module: null
sensitivity: normal
name: member status operate(t_member_status_operate)
aliases:
- t_member_status_operate
related_services:
- svc_aml
related_scenarios: []
---
# member status operate(t_member_status_operate)

## 用途
member status operate。属 amlrisk 库,由 [[svc_aml]] 读写。

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
| `operate_type` | varchar(20) | NOT NULL | operate type:Lock_Member,UnLock_Member,Deny_Out_Account,Deny_In_Account,Freeze_Account,UnFreeze_Account |
| `source` | varchar(20) | NOT NULL | source:Compliance_Auto,Compliance_Manual,Risk_Auto,Risk_Manual |
| `operator` | varchar(50) | NOT NULL | default:system |
| `status` | char | NOT NULL / 默认 'I' | status: Y=Success,N=NoNeed,I=Init |
| `notify_flag` | char | NOT NULL / 默认 'N' | N:No,Y:Yes |
| `notify_status` | char | NOT NULL / 默认 'N' | N:No,Y:Yes |
| `before_status` | varchar(10) |  | before status |
| `after_status` | varchar(10) |  | after status |
| `remark` | varchar(255) |  | remark |
| `extension` | varchar(255) |  | extension |
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
