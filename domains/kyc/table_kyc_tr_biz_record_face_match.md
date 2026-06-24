---
id: tbl_kyc_tr_biz_record_face_match
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
- biz-record
- tr_biz_record_face_match
subdomain: biz-record
module: null
sensitivity: sensitive
name: Face match table(tr_biz_record_face_match)
aliases:
- tr_biz_record_face_match
related_services:
- svc_kyc
related_scenarios: []
---

# Face match table(tr_biz_record_face_match)

## 用途
**人脸比对结果**:活体照(check image)与证件照/底库的比对分数(`match_score`)与通道返回。`record_id`/`req_token` 关联主流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | Primary key ID |
| `record_id` | bigint | NOT NULL | Biz record id |
| `req_token` | varchar(32) | NOT NULL | Kyc flow token |
| `req_idn` | varchar(35) |  | Eid number |
| `req_check_image` | varchar(55) |  | Check image |
| `channel_code` | varchar(55) |  | Channel code |
| `match_score` | varchar(10) |  | Live face score |
| `resp_code` | varchar(32) |  | Response code |
| `resp_msg` | varchar(1024) |  | Response Msg |
| `memo` | varchar(255) |  | Memo |
| `exp` | varchar(32) |  | Extended |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_rid`:(`record_id`)
- 索引 `idx_token`:(`req_token`)

## 校验点(QA 关注)
- `match_score` 阈值判定;低分应拒绝/转人审。
- `req_idn`/check image 敏感,密文/tag。
