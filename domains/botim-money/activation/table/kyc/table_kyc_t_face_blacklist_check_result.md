---
id: tbl_kyc_t_face_blacklist_check_result
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
- risk
- t_face_blacklist_check_result
subdomain: risk
module: null
sensitivity: restricted
name: 比对结果记录(t_face_blacklist_check_result)
aliases:
- t_face_blacklist_check_result
related_services:
- svc_kyc
related_scenarios: []
---

# 比对结果记录(t_face_blacklist_check_result)

## 用途
**人脸黑名单比对结果**:比对记录(`check_record_id`→check_record)对应的明细结果(分数/特征/结论)。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | 主键 |
| `check_record_id` | bigint(32) | NOT NULL | 比对记录ID |
| `member_id` | varchar(22) |  | 会员ID |
| `face_score` | varchar(6) |  | 比对分数 |
| `feature_id` | varchar(32) | NOT NULL | 特征ID |
| `result` | char | NOT NULL | 比对结果 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_feature_id`:(`feature_id`)
- 索引 `idx_member_id`:(`member_id`)
- 索引 `idx_record_id`:(`check_record_id`)

## 校验点(QA 关注)
- `face_score`/`result` 与 check_record.check_result 一致。
- feature_id 可追溯到 t_face_blacklist。
