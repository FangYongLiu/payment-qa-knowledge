---
id: tbl_kyc_tr_biz_record_dependency
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
- biz-record
- tr_biz_record_dependency
subdomain: biz-record
module: null
sensitivity: normal
name: tr_biz_record_dependency(tr_biz_record_dependency)
aliases:
- tr_biz_record_dependency
related_services:
- svc_kyc
related_scenarios: []
---

# tr_biz_record_dependency(tr_biz_record_dependency)

## 用途
**外部依赖调用记录**:KYC 流程中对外部系统(如风控 RR-risk rating)的调用结果。`record_id`/`req_token` 关联主流程,`dependency_type` 标识依赖类型。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | ID:8+9 |
| `record_id` | bigint(22) |  |  |
| `req_token` | varchar(32) | NOT NULL | Process TOKEN |
| `dependency_type` | varchar(15) |  | Dependency Type：RR-risk rating |
| `member_id` | varchar(20) |  | member id |
| `return_code` | varchar(35) |  | Api Return Code |
| `return_msg` | varchar(225) |  | Api Return Msg |
| `result_status` | varchar(22) |  | Api Return Status |
| `extension` | varchar(200) |  | Extension |
| `memo` | varchar(64) |  | Memo |
| `result_time` | timestamp |  | Api Result Time |
| `create_time` | timestamp |  | Create Time |
| `update_time` | timestamp |  | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_member_id`:(`member_id`)
- 索引 `idx_record_id`:(`record_id`)
- 索引 `idx_token`:(`req_token`)

## 校验点(QA 关注)
- `dependency_type`(RR 等) 与下游服务对应;`result_status`/`return_code` 决定流程是否放行。
- 风控拦截路径(见 tm_biz_access_records.status=3)联动。
