---
id: tbl_kyc_tr_biz_record_passport
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
- passport
- tr_biz_record_passport
subdomain: passport
module: null
sensitivity: restricted
name: 护照业务记录表(tr_biz_record_passport)
aliases:
- tr_biz_record_passport
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_zand_iban
---

# 护照业务记录表(tr_biz_record_passport)

## 用途
**护照 OCR 业务记录**:护照信息页识别出的护照号/类型/国籍/姓名/有效期/MRZ/行业等。`record_id`/`req_token` 关联主流程。对应 passport submit/submit-ocr 类接口。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_zand_iban]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(35) | PK / NOT NULL | 主键ID |
| `record_id` | bigint(35) | NOT NULL | 业务记录ID |
| `req_token` | varchar(32) | NOT NULL | 流程token |
| `req_file_name` | varchar(128) | NOT NULL | 护照信息页 |
| `req_avatar_tag` | varchar(35) |  | 护照头像tag |
| `ocr_channle_code` | varchar(128) |  | ocr渠道码 |
| `ocr_passport_type` | varchar(32) |  | 护照类型 |
| `ocr_passport_nationality` | varchar(200) |  | 护照国籍 |
| `ocr_passport_country_code` | varchar(20) |  | 国家码 |
| `ocr_passport_name` | varchar(200) |  | 姓名 |
| `ocr_passport_no` | varchar(200) |  | 护照编号 |
| `ocr_passport_birth_date` | datetime |  | 出生日期 |
| `ocr_passport_gender` | varchar(20) |  | 性别 |
| `ocr_passport_address` | varchar(200) |  | 住址地址 |
| `ocr_passport_expiry_date` | datetime |  | 护照有效期 |
| `ocr_issue_date` | datetime |  | 护照颁发日期 |
| `ocr_issue_place` | varchar(155) |  | Ocr issueplace |
| `ocr_mrz` | varchar(100) |  | Ocr mrz |
| `industry` | varchar(85) |  | 行业信息 |
| `extension` | varchar(255) |  | Extension |
| `resp_code` | varchar(32) |  | 响应编码 |
| `resp_msg` | varchar(250) |  | 响应信息 |
| `invitation_code` | varchar(32) |  | 邀请码 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_rid`:(`record_id`)

## 校验点(QA 关注)
- `ocr_passport_no` 等敏感字段密文。
- 护照有效期 `ocr_passport_expiry_date` 用于过期判断与 tm_pp_expiry_notify_event 一致。
- 识别失败 resp_code 记录;v1/v2/signzy 通道差异(见 flow_type)。
