---
id: tbl_kyc_tr_biz_record_ica
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
- eid
- tr_biz_record_ica
subdomain: eid
module: null
sensitivity: sensitive
name: ICA业务记录表(tr_biz_record_ica)
aliases:
- tr_biz_record_ica
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
---

# ICA业务记录表(tr_biz_record_ica)

## 用途
EID **ICA 政府核验结果**:向 ICA 通道核验证件真实性,落 unified_no/姓名(中英阿)/国籍/婚姻/护照等权威字段。`record_id` 关联 tm_biz_record。是 EID 实名的权威数据来源。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `record_id` | bigint |  | KYC业务记录ID |
| `req_full_name` | varchar(64) |  | 全名 |
| `req_eid` | varchar(32) |  | EID |
| `req_nationality` | varchar(32) |  | OCR识别的国籍 |
| `req_date_of_birth` | datetime |  | 出生日期 |
| `req_sex` | varchar(32) |  | 性别 |
| `req_industry` | varchar(175) |  | 行业信息 |
| `req_token` | varchar(32) |  | 请求token |
| `req_manual` | varchar(32) |  | 是否为手工 |
| `req_manual_attr` | varchar(55) |  | Manual modify attribute |
| `req_expiry_date` | timestamp |  | 过期日期 |
| `req_partner_id` | varchar(32) |  | 平台ID |
| `ica_unified_no` | varchar(32) |  | 证件唯一编号 |
| `ica_idn` | varchar(32) |  | 身份证号 |
| `ica_name_arabic` | varchar(32) |  | 阿拉伯名称 |
| `ica_name_english` | varchar(32) |  | 英文名称 |
| `ica_family_name_ar` | varchar(150) |  | ica阿语姓 |
| `ica_family_name_en` | varchar(150) |  | ica英语姓 |
| `ica_nationality_ica` | varchar(32) |  | 通道返回国籍 |
| `ica_nationality_code` | char(3) |  | 国籍alpha3 |
| `ica_nationality_desc` | varchar(32) |  | 通道返回国籍描述 |
| `ica_birth_date` | datetime |  | 出生日期 |
| `ica_marital_status` | varchar(32) |  | 婚姻状态 |
| `ica_religion` | varchar(32) |  | 信仰 |
| `ica_home_land` | varchar(32) |  | 户籍 |
| `ica_gender` | varchar(32) |  | 性别 |
| `ica_mobile_no` | varchar(25) |  | ICA mobile number |
| `ica_channel_code` | varchar(32) |  | 通道编号 |
| `ica_eid_expiry_date` | varchar(25) |  | eid过期时间 |
| `ica_passport_type` | varchar(35) |  | 护照类型 |
| `ica_passport_nationality_desc` | varchar(255) |  | 护照国籍 |
| `ica_passport_no` | varchar(50) |  | 护照编号(加密) |
| `ica_passport_expiry_date` | varchar(25) |  | 护照过期时间 |
| `resp_code` | varchar(32) |  | 响应编码 |
| `resp_msg` | varchar(255) |  | 响应详细 |
| `exp1` | varchar(32) |  | 扩展字段1 |
| `exp2` | varchar(32) |  | 扩展字段2 |
| `create_time` | timestamp |  | 创建日期 |
| `update_time` | timestamp |  | 更新日期 |
| `ica_id_card_no` | varchar(35) |  | 卡片号 |
| `ica_issue_date` | varchar(32) |  | ICP issue date |
| `ica_issue_place` | varchar(128) |  | ICP issue place |
| `ica_certificate` | varchar(100) |  | ICP certificate |
| `ica_person_face` | varchar(64) |  | ICP Return Person Face |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_rid`:(`record_id`)

## 校验点(QA 关注)
- ICA 返回字段与 OCR 识别结果一致性(姓名/国籍/有效期)。
- `resp_code` 非成功时不得据此通过实名。
- 敏感证件字段密文;`req_manual`=手工修正路径需单独校验。
