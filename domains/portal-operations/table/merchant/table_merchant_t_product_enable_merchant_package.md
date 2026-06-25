---
id: tbl_merchant_t_product_enable_merchant_package
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_product_enable_merchant_package
subdomain: merchant
module: null
sensitivity: normal
name: Merchant product enablement and rate configuration table(t_product_enable_merchant_package)
aliases:
- t_product_enable_merchant_package
related_services:
- svc_merchant
related_scenarios: []
---
# Merchant product enablement and rate configuration table(t_product_enable_merchant_package)

## 用途
Merchant product enablement and rate configuration table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `merchant_mid` | varchar(32) | NOT NULL | Merchant MID |
| `merchant_name` | varchar(64) | NOT NULL | Merchant Name |
| `partner_id` | varchar(32) | NOT NULL | Partner ID |
| `package_code` | varchar(64) | NOT NULL | Package Code |
| `package_name` | varchar(64) |  | Package Name |
| `package_type` | varchar(16) |  | Package Type |
| `settlement_type` | varchar(2) | NOT NULL / 默认 'R' | Settlement Type |
| `settlement_cycle` | int | 默认 1 | Settlement Cycle |
| `charger` | decimal(18,6) | 默认 0 | charger |
| `strategy_type` | int | 默认 3 | Strategy Type |
| `calculation_attr` | varchar(255) |  | Calculation Attributes (JSON) |
| `fix_charge` | decimal(18,6) | 默认 0 | Fixed Charge Amount |
| `fix_rate` | decimal(18,6) | 默认 0 | Fixed Charge Rate |
| `min_charge` | decimal(18,6) | 默认 0 | Minimum Charge Amount |
| `max_charge` | decimal(18,6) | 默认 0 | Maximum Charge Amount |
| `status` | varchar(16) | 默认 'INIT' | Status |
| `gmt_effective` | timestamp |  | Effective Time |
| `gmt_invalid` | timestamp |  | Expiration Time |
| `retry_count` | int | 默认 0 | Retry Count |
| `max_retries` | int | 默认 0 | Maximum Retries |
| `processed_time` | timestamp |  | Actual processing time |
| `error_message` | varchar(255) |  | Error details if failed |
| `created_time` | timestamp |  | Created time |
| `last_updated_time` | timestamp |  | Last updated time |
| `version` | int | 默认 0 | Data version |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_mid_package` (merchant_mid, package_code)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
