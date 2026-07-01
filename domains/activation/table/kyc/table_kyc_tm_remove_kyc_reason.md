---
id: tbl_kyc_tm_remove_kyc_reason
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- lifecycle
- tm_remove_kyc_reason
subdomain: lifecycle
module: null
sensitivity: normal
name: Remove Kyc Reason Table(tm_remove_kyc_reason)
aliases:
- tm_remove_kyc_reason
related_services:
- svc_kyc
related_scenarios: []
---

# Remove Kyc Reason Table(tm_remove_kyc_reason)

## 用途
**删除 KYC 原因表**:删除/移除实名时记录原因(AUTO/MANUAL + code + 描述),`apply_id` 关联流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK | Primary Key |
| `apply_id` | bigint | NOT NULL | Apply ID |
| `member_id` | varchar(32) | NOT NULL | Member ID |
| `type` | varchar(15) | NOT NULL | Reason Type: AUTO, MANUAL |
| `code` | varchar(35) | NOT NULL | Reason Code |
| `reason` | varchar(255) | NOT NULL | Reason Description |
| `operator` | varchar(100) |  | Operator |
| `memo` | varchar(255) |  | Memo |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_apply_id`:(`apply_id`)
- 索引 `idx_mid`:(`member_id`)

## 校验点(QA 关注)
- `type`(AUTO/MANUAL) 与 code/reason 对应。
- 删除动作应同时落 tm_kyc_activity_log。
