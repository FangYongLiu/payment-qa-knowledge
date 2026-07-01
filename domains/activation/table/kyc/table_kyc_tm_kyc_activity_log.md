---
id: tbl_kyc_tm_kyc_activity_log
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
- tm_kyc_activity_log
subdomain: lifecycle
module: null
sensitivity: normal
name: Kyc Activity Log Table(tm_kyc_activity_log)
aliases:
- tm_kyc_activity_log
related_services:
- svc_kyc
related_scenarios: []
---

# Kyc Activity Log Table(tm_kyc_activity_log)

## 用途
**KYC 活动日志**:实名生命周期关键动作流水(EID/护照 完成/续期/删除),`apply_id` 关联流程。审计与回溯。

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
| `type` | varchar(25) | NOT NULL | Operation Type: EID_KYC_FINISH, EID_KYC_RENEW, EID_KYC_DELETE, PP_KYC_FINISH,PP_KYC_DELETE |
| `reason` | varchar(255) | NOT NULL | Operation Reason |
| `result` | varchar(255) |  | Operation Result |
| `operator` | varchar(100) |  | Operator |
| `memo` | varchar(255) |  | Memo |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_apply_id`:(`apply_id`)
- 索引 `idx_mid`:(`member_id`)

## 校验点(QA 关注)
- `type`(EID_KYC_FINISH/RENEW/DELETE/PP_*) 与实际动作一致。
- 每个关键动作都应有日志;operator/result 留痕。
