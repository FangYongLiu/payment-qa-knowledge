---
id: tbl_kyc_tm_audit_log
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
- audit
- tm_audit_log
subdomain: audit
module: null
sensitivity: normal
name: 审核任务表(tm_audit_log)
aliases:
- tm_audit_log
related_services:
- svc_kyc
related_scenarios: []
---

# 审核任务表(tm_audit_log)

## 用途
**审核操作日志**:对审核任务(`audit_id`→tm_audit_task)的每次操作留痕(审核人/结果/类型/备注)。审计轨迹。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `audit_id` | bigint |  | 审核任务表ID |
| `audit_user` | varchar(32) |  | 审核人员 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |
| `log_type` | varchar(32) |  | 日志类型 |
| `audit_result` | varchar(32) |  | 审核人员 |
| `exp1` | varchar(32) |  | 扩展字段1 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_audit_id`:(`audit_id`)

## 校验点(QA 关注)
- 每次审核动作都应有 log;`audit_result` 与 task 终态一致。
- 审核人 audit_user 与权限。
