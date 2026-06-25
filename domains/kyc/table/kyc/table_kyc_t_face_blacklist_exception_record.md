---
id: tbl_kyc_t_face_blacklist_exception_record
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
- risk
- t_face_blacklist_exception_record
subdomain: risk
module: null
sensitivity: restricted
name: 比对异常记录(t_face_blacklist_exception_record)
aliases:
- t_face_blacklist_exception_record
related_services:
- svc_kyc
related_scenarios: []
---

# 比对异常记录(t_face_blacklist_exception_record)

## 用途
**人脸黑名单比对异常记录**:比对异常(`result`=E)的记录与重试(`retry_times`),`check_record_id` 关联比对记录。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | 主键 |
| `check_record_id` | bigint(32) | NOT NULL | 比对记录ID |
| `member_id` | varchar(20) | NOT NULL | 会员ID |
| `face_tag` | varchar(128) | NOT NULL | 被比对的人脸照片 |
| `exp_black_id` | bigint(32) |  | 比对异常的名单ID |
| `exp_face_tag` | varchar(128) |  | 比对异常的照片 |
| `result` | char | NOT NULL | 比对结果（E:比对异常，S：完成） |
| `retry_times` | int | NOT NULL | 重试次数 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_member_id`:(`member_id`)
- 索引 `idx_record_id`:(`check_record_id`)

## 校验点(QA 关注)
- 异常应按 retry_times 重试;超限转人工。
- exp_black_id/exp_face_tag 定位异常名单。
