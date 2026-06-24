---
id: tbl_kyc_tr_biz_record_customer_detail
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
- tr_biz_record_customer_detail
subdomain: biz-record
module: null
sensitivity: sensitive
name: Customer detail(tr_biz_record_customer_detail)
aliases:
- tr_biz_record_customer_detail
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_zand_iban
---

# Customer detail(tr_biz_record_customer_detail)

## 用途
**Signzy 渠道客户详情**:signzy full journey 返回的完整客户画像(护照/签证/移民/居住/担保人/出行等原始分段),`apply_id` 关联 tm_kyc_apply。EID/护照 full journey 的 raw 落库。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_zand_iban]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | Primary key |
| `apply_id` | bigint | NOT NULL | Kyc apply id |
| `member_id` | varchar(20) | NOT NULL | Member ID |
| `journey_info` | varchar(1150) |  | Raw channel response sections (capturedData / documentExtraction / selfieAnalysis / verificationLevel) |
| `personal_info` | varchar(1024) |  | Personal Info |
| `active_passport` | varchar(1024) |  | Active Passport |
| `documents` | varchar(1024) |  | Digital documents (EID / signature / face photo in base64) |
| `immigration_file` | varchar(1024) |  | Immigration file information |
| `person_contact_details` | varchar(1024) |  | Personal contact details |
| `residence_info` | varchar(1024) |  | Residence information |
| `sponsor_contact_details` | varchar(1024) |  | Sponsor contact details |
| `sponsor_details` | varchar(1024) |  | Sponsor details |
| `travel_detail` | varchar(1024) |  | Travel record |
| `active_visa` | varchar(1024) |  | Active Visa |
| `source_association_details` | varchar(1024) |  | Source association details |
| `extension` | varchar(255) |  | Extension |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `apply_id_idx`:(`apply_id`)
- 索引 `mid_idx`:(`member_id`)

## 校验点(QA 关注)
- 各 JSON 分段长度上限(varchar(1024/1150))截断风险。
- documents 含 base64(EID/签名/人脸),敏感,访问控制。
- journey_info 与 personal_info 等解析结果一致。
