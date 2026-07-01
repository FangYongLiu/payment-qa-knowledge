---
id: tbl_kyc_tr_biz_record_ocr
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
- eid
- tr_biz_record_ocr
subdomain: eid
module: null
sensitivity: restricted
name: OCR业务记录表(tr_biz_record_ocr)
aliases:
- tr_biz_record_ocr
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
---

# OCR业务记录表(tr_biz_record_ocr)

## 用途
EID **OCR 识别结果**:身份证正反面识别出的 idn/姓名/国籍/性别/有效期/MRZ 等。`record_id` 关联 tm_biz_record,`req_token` 关联流程 token。对应 submit-ocr/submit-edit 类接口。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `record_id` | bigint |  | KYC业务记录ID |
| `req_token` | varchar(32) |  | kcy流程token |
| `req_front_file_name` | varchar(128) |  | 身份证正面 |
| `req_back_file_name` | varchar(128) |  | 身份证反面 |
| `ocr_idn` | varchar(32) |  | 身份证号 |
| `ocr_cert_no` | varchar(32) |  | 证件号 |
| `ocr_name` | varchar(32) |  | 姓名 |
| `ocr_name_arabic` | varchar(35) |  | Ocr name arabic |
| `ocr_family_name_en` | varchar(55) |  | Ocr family name en |
| `ocr_family_name_ar` | varchar(55) |  | Ocr family name ar |
| `ocr_nationality` | varchar(32) |  | 国籍 |
| `ocr_nationality_code` | varchar(5) |  | Ocr nationality code |
| `ocr_gender` | varchar(32) |  | 性别 |
| `ocr_birth_date` | datetime |  | 出生日期 |
| `ocr_start_date` | timestamp |  | 证件启用日期 |
| `ocr_expiry_date` | timestamp |  | 证件过期日期 |
| `ocr_channle_code` | varchar(32) |  | 通道编号 |
| `ocr_mrz_text` | varchar(255) |  | eid背面防伪串 |
| `mrz_tag` | varchar(55) |  | eid条码识别标记 |
| `resp_code` | varchar(32) |  | 响应编码 |
| `resp_msg` | varchar(255) |  | 响应信息 |
| `invitation_code` | varchar(32) |  | 邀请码 |
| `occupation` | varchar(125) |  | 职位 |
| `employer` | varchar(125) |  | 雇主 |
| `issue_place` | varchar(125) |  | 签发地 |
| `issue_date` | timestamp |  | 签发日期 |
| `issuer` | varchar(15) |  | 签发者 |
| `signature_photo` | varchar(125) |  | 签名照 |
| `portrait` | varchar(55) |  | Portrait |
| `exp1` | varchar(32) |  | 扩展字段1 |
| `exp2` | varchar(455) |  | 扩展字段2 |
| `create_time` | timestamp |  | 创建日期 |
| `update_time` | timestamp |  | 更新日期 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_ocr_front`:(`req_front_file_name`)
- 索引 `idx_rid`:(`record_id`)

## 校验点(QA 关注)
- `ocr_idn`/证件号等敏感字段应为**密文**存储。
- 识别失败时 `resp_code`/`resp_msg` 记录原因,正常流程不应进入下一步。
- `ocr_expiry_date` 用于后续 EID 过期判断,需与 ICA 核验结果一致。
