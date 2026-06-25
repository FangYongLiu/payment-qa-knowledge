---
id: tbl_kyc_tm_audit_task
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
- audit
- tm_audit_task
subdomain: audit
module: null
sensitivity: restricted
name: 审核任务表(tm_audit_task)
aliases:
- tm_audit_task
related_services:
- svc_kyc
related_scenarios: []
---

# 审核任务表(tm_audit_task)

## 用途
**人工审核任务表**:免审不过/命中规则时转人工,记录审核节点(node_type)、触发原因(reason)、申请人、审核人与状态。`relation_id` 关联流程记录。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `relation_id` | bigint |  | 流程记录关联ID |
| `member_id` | varchar(32) |  | 会员ID |
| `task_type` | varchar(32) |  | 任务类型 |
| `node_type` | varchar(32) |  | 审核节点信息 |
| `status` | varchar(2) |  | 本次kyc流程的状态 |
| `mobile` | varchar(32) |  | 手机号 |
| `apply_name` | varchar(120) |  | 申请人 |
| `task_tag` | varchar(255) |  | 标签记录 |
| `referrer` | varchar(35) |  | 推荐人手机 |
| `source` | varchar(35) |  | 做kyc客户端来源 |
| `audit_user` | varchar(75) |  | 审核人 |
| `reason` | varchar(255) |  | 触发审核原因 |
| `reason_msg` | varchar(385) |  | reason message |
| `eid` | varchar(35) |  | 用户eid |
| `memo` | varchar(200) |  | Memo |
| `create_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_relation_id`:(`relation_id`)

## 校验点(QA 关注)
- 触发人审的 `reason`/`reason_msg` 与风控/比对结果对应。
- `status`/`node_type` 流转;审核结论回写主流程 status。
- 审核人 audit_user 权限与操作审计(tm_audit_log)。
