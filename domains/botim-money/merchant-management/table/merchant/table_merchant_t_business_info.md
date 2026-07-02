---
id: tbl_merchant_t_business_info
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
- t_business_info
subdomain: merchant
module: null
sensitivity: normal
name: 商户经营信息(t_business_info)
aliases:
- t_business_info
related_services:
- svc_merchant
related_scenarios: []
---
# 商户经营信息(t_business_info)

## 用途
商户经营信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC |  |
| `merchant_creation_id` | bigint | NOT NULL | Merchant Creation Id |
| `number_of_employees` | int |  | Number of Employees |
| `number_of_branches` | int |  | Number of Branches |
| `customer_type` | varchar(100) |  | Customer Type |
| `primary_currency` | char(3) |  | Primary Currency |
| `customer_countries` | varchar(255) |  | Customer Countries |
| `expected_non_card_sales` | decimal(15,2) |  | Expected Non Card Sales |
| `card_present_pos` | varchar(10) |  | Card Present POS |
| `card_present_in_store` | varchar(10) |  | Card Present In-Store |
| `monthly_pos_sales` | decimal(15,2) |  | Monthly POS Sales |
| `monthly_gateway_sales` | decimal(15,2) |  | Monthly Gateway Sales |
| `delivery_timeline` | varchar(25) |  | Delivery Timeline |
| `delivery_channels` | varchar(100) |  | Delivery Channels |
| `signature_path` | varchar(255) |  | Signature Path |
| `shop_photo_path` | varchar(255) |  | Shop Photo Path |
| `tenancy_contract_path` | varchar(255) |  | Tenancy Contract Path |
| `share_reg_path` | varchar(255) |  | Share Reg Path |
| `created_time` | timestamp | 默认 CURRENT_TIMESTAMP | Created At Time |
| `last_updated_time` | timestamp | 默认 CURRENT_TIMESTAMP | Last Updated Time |
| `data_version` | bigint | 默认 1 | Data version for concurrency control |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_creation_id` (merchant_creation_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
