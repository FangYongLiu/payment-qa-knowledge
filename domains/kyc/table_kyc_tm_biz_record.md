---
id: tbl_kyc_tm_biz_record
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
- tm_biz_record
subdomain: biz-record
module: null
sensitivity: restricted
name: KYC业务记录基础表(tm_biz_record)
aliases:
- tm_biz_record
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
---

# KYC业务记录基础表(tm_biz_record)

## 用途
KYC **业务记录基础表**:一次 apply 下每个业务环节(OCR/活体/ICA/验证/护照…)的主记录,`apply_id` 关联 [[tbl_kyc_tm_kyc_apply]]。各 `tr_biz_record_*` 明细子表通过 `record_id` 反挂本表 `id`,`biz_type` 标识环节类型。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `apply_id` | bigint |  | kyc业务流程ID |
| `member_id` | varchar(32) |  | 会员ID |
| `biz_type` | varchar(32) |  | 业务类型 |
| `status` | int |  | 记录状态 |
| `code` | varchar(32) |  | 处理结果码 |
| `message` | varchar(255) |  | 处理结果信息 |
| `operation_type` | varchar(32) |  | 操作类型 |
| `create_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_applyid_mid_type`:(`apply_id`, `member_id`, `biz_type`)
- 索引 `idx_create_time`:(`create_time`)
- 索引 `idx_member_id`:(`member_id`)

## 校验点(QA 关注)
- `apply_id` 必须能回到 tm_kyc_apply;`record_id`(子表)= 本表 id。
- `biz_type` 与实际写入的子表类型对应(OCR→tr_biz_record_ocr 等)。
- `status`/`code`/`message` 与子表 resp_code/resp_msg 一致。
