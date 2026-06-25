---
id: tbl_kyc_tr_biz_record_verify
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
- tr_biz_record_verify
subdomain: eid
module: null
sensitivity: restricted
name: 身份证验证表(tr_biz_record_verify)
aliases:
- tr_biz_record_verify
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
---

# 身份证验证表(tr_biz_record_verify)

## 用途
EID **身份证验证表**:把请求侧(req_*)与通道返回侧(resp_*)的姓名/EID/国籍/出生/性别逐项比对落库,对应 verify-again 类接口。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `record_id` | bigint |  | 业务记录ID |
| `req_full_name` | varchar(32) |  | 全名 |
| `req_eid` | varchar(32) |  | EID |
| `req_nationality` | varchar(32) |  | OCR识别的国籍 |
| `req_date_of_birth` | datetime |  | 出生日期 |
| `req_sex` | varchar(32) |  | 性别 |
| `resp_name_english` | varchar(32) |  | 全名 |
| `resp_idn` | varchar(32) |  | EID |
| `resp_nationality` | varchar(32) |  | OCR识别的国籍 |
| `resp_birth_date` | datetime |  | 出生日期 |
| `resp_gender` | varchar(32) |  | 性别 |
| `resp_code` | varchar(32) |  | 响应编码 |
| `resp_msg` | varchar(255) |  | 响应详细 |
| `exp1` | varchar(32) |  | 扩展字段1 |
| `exp2` | varchar(32) |  | 扩展字段2 |
| `create_time` | timestamp |  | 创建日期 |
| `update_time` | timestamp |  | 更新日期 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- req_* 与 resp_* 逐字段一致性即为验证结果依据。
- 不一致时 `resp_code` 标记;敏感字段密文。
