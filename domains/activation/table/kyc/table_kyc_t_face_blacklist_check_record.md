---
id: tbl_kyc_t_face_blacklist_check_record
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
- t_face_blacklist_check_record
subdomain: risk
module: null
sensitivity: restricted
name: 命中黑名单记录(t_face_blacklist_check_record)
aliases:
- t_face_blacklist_check_record
related_services:
- svc_kyc
related_scenarios: []
---

# 命中黑名单记录(t_face_blacklist_check_record)

## 用途
**人脸黑名单比对记录**:每次拿待比对人脸去黑名单比对的记录,`status`(待比对/比对中/异常/完成),`check_result`(命中/未命中)。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | 主键 |
| `blacklist_id` | bigint(32) |  | 黑名单ID |
| `face_tag` | varchar(128) | NOT NULL | 被比对的人脸照片 |
| `member_id` | varchar(20) |  | 被比对的会员ID |
| `idn` | varchar(55) |  | 被比对的证件号密文 |
| `mobile` | varchar(55) |  | 手机号（密文掩码） |
| `status` | char | NOT NULL | 状态（I:待比对，P:比对中，E：比对异常，S：比对完成） |
| `check_result` | char |  | 比对结果（0:未命中，1：命中） |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_create_time`:(`create_time`)
- 索引 `idx_mid`:(`member_id`)

## 校验点(QA 关注)
- `status` 流转;命中(check_result=1) 应联动拦截/人审。
- 比对结果落 t_face_blacklist_check_result;异常落 _exception_record。
