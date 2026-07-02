---
id: tbl_aml_t_member_limit_manual_apply
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
- t_member_limit_manual_apply
subdomain: aml
module: null
sensitivity: normal
name: Limit Manual Apply(t_member_limit_manual_apply)
aliases:
- t_member_limit_manual_apply
related_services:
- svc_aml
related_scenarios: []
---
# Limit Manual Apply(t_member_limit_manual_apply)

## 用途
Limit Manual Apply。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `id_no` | varchar(20) |  | Id No |
| `member_id` | varchar(20) |  | Member Id |
| `limit_amount` | decimal(15,4) |  | Limit Amount |
| `salary` | decimal(15,4) |  | Salary |
| `currency` | varchar(8) | NOT NULL | Currency |
| `reason` | varchar(255) |  | Reason |
| `status` | varchar(25) |  | Status |
| `notify_status` | varchar(2) |  | Notify Status I-Init S-Submit F-Fail |
| `apply_user` | varchar(50) |  | Apply User |
| `apply_type` | varchar(10) |  | Apply Type:MR-Manual Request  AA-Admin Action |
| `memo` | varchar(255) |  | Memo |
| `extension` | varchar(255) |  | Extension |
| `documents` | varchar(255) |  | Document List |
| `create_time` | timestamp(3) |  | Create Time |
| `update_time` | timestamp(3) |  | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_id_no` (id_no)
  - `idx_member_id` (member_id)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
