---
id: tbl_merchant_t_sub_merchant
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_sub_merchant
subdomain: merchant
module: null
sensitivity: normal
name: Sub merchant table aligned with domain model and API structure(t_sub_merchant)
aliases:
- t_sub_merchant
related_services:
- svc_merchant
related_scenarios: []
---
# Sub merchant table aligned with domain model and API structure(t_sub_merchant)

## 用途
Sub merchant table aligned with domain model and API structure。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Unique identifier for SubMerchant |
| `pay_facs` | varchar(50) | NOT NULL | Parent payment facilitator (PayFac) identifier linked to this SubMerchant |
| `sub_merchant_id` | varchar(50) | NOT NULL | Submerchant Unique identifier (business identifier) |
| `bank_industry_code` | varchar(20) |  | Bank industry code of the SubMerchant (e.g., NAICS/SIC) |
| `trading_name` | varchar(100) |  | Trading name or DBA name of the SubMerchant |
| `registered_name` | varchar(100) |  | Official registered name of the SubMerchant |
| `city` | varchar(50) |  | City where the SubMerchant operates |
| `country` | varchar(10) |  | Country where the SubMerchant operates (ISO Alpha-2) |
| `phone` | varchar(20) |  | Contact phone number for the SubMerchant |
| `email` | varchar(50) |  | Email address for the SubMerchant |
| `dispute_contact_phone` | varchar(20) |  | Dedicated dispute contact phone number for the SubMerchant |
| `marketplace_id` | varchar(50) |  | Marketplace identifier associated with the SubMerchant |
| `government_country_code` | varchar(10) |  | Government-issued country code (ISO 3166-1 alpha-3) |
| `first_trading_time` | timestamp |  | First trading activity timestamp of the SubMerchant |
| `last_trading_time` | timestamp |  | Last trading activity timestamp of the SubMerchant |
| `compliance_status` | varchar(50) | NOT NULL | Compliance status of the SubMerchant |
| `sicmcc` | varchar(10) |  | SIC or MCC code related to SubMerchant |
| `status` | varchar(20) |  | Operational status of the SubMerchant |
| `created_time` | timestamp | 默认 CURRENT_TIMESTAMP | Timestamp when the SubMerchant record was created |
| `updated_time` | timestamp | 默认 CURRENT_TIMESTAMP | Timestamp when the SubMerchant record was last updated |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_payfacs_submerchant` 唯一 (pay_facs, sub_merchant_id)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
