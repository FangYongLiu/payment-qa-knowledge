---
id: tbl_remittance_t_beneficiary_identity_info
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_beneficiary_identity_info
subdomain: remittance
module: null
sensitivity: normal
name: 受益人身份信息(t_beneficiary_identity_info)
aliases:
- t_beneficiary_identity_info
related_services:
- svc_remittance
related_scenarios: []
---
# 受益人身份信息(t_beneficiary_identity_info)

## 用途
受益人身份信息。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `relation_beneficiary_id` | bigint |  | 关联来源受益人id |
| `identity` | varchar(32) |  | 受益人所属平台ID |
| `member_id` | varchar(20) | NOT NULL | 受益人所属会员id |
| `source` | varchar(20) | NOT NULL | 受益人添加来源 |
| `partner_id` | varchar(20) | NOT NULL | 受益人来源平台 |
| `transaction_mode` | varchar(64) | NOT NULL | 服务模式:BANK_TRANSFER|CASH_PICK_UP |
| `first_name` | varchar(255) | NOT NULL | 名 |
| `middle_name` | varchar(255) |  | 中间名 |
| `last_name` | varchar(255) | NOT NULL | 姓 |
| `nickname` | varchar(32) |  | 昵称 |
| `id_type` | varchar(12) |  | 证件类型，如EID |
| `id_number` | varchar(32) |  | 证件号 |
| `mobile_no` | varchar(32) |  | 手机号 |
| `mobile_country` | char(3) |  | 手机号国家;手机号所属国家 |
| `birth_date` | date |  | 生日 |
| `gender` | char |  | 性别 |
| `nationality` | char(3) |  | 受益人国籍ISO code |
| `email` | varchar(64) |  | 邮箱 |
| `profession` | varchar(12) |  | 职业 |
| `relation_ship` | varchar(32) |  | 受益人关系 |
| `customer_classification` | varchar(255) |  | 客户分类JSON |
| `additional_info` | varchar(255) |  | 额外信息;JSON,一般为需要补充的信息 |
| `is_default` | char |  | 是否默认受益人;Y:是；N：否 |
| `enable_flag` | char | NOT NULL | 启用标识: Y=启用，N=停用 |
| `unity_id` | varchar(32) |  | 唯一识别 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `unity_code` | varchar(25) |  | 风控返回结果 |
| `aml_status` | varchar(2) |  | W 等待提交; SW 提交风控未审核; SP 提交审核通过; SR 提交审核拒绝; SE 提交风控异常 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_unity_id` 唯一 (unity_id)
- 索引:
  - `idx_ben_id_mid` (member_id)
  - `idx_create_time` (create_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
