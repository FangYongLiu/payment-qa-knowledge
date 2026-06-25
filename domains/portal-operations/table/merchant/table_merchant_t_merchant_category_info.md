---
id: tbl_merchant_t_merchant_category_info
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
- t_merchant_category_info
subdomain: merchant
module: null
sensitivity: normal
name: Merchant Category Audit Table(t_merchant_category_info)
aliases:
- t_merchant_category_info
related_services:
- svc_merchant
related_scenarios: []
---
# Merchant Category Audit Table(t_merchant_category_info)

## 用途
Merchant Category Audit Table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | ID |
| `merchant_mid` | varchar(32) | NOT NULL | Merchant Mid |
| `merchant_name` | varchar(100) | NOT NULL | Merchant name |
| `category_id` | varchar(32) | NOT NULL | Category ID |
| `mcc_code` | varchar(6) | NOT NULL | Merchant category code |
| `mcc_name` | varchar(200) | NOT NULL | Merchant category name |
| `description` | varchar(500) |  | Description |
| `product_percentage` | varchar(500) |  | Product Percentage |
| `apply_type` | varchar(32) | NOT NULL | Type of Application |
| `applicant` | varchar(32) | NOT NULL | Name of Applicant |
| `status` | varchar(32) | NOT NULL | Approval Status |
| `auditor` | varchar(32) |  | Auditor for Category Process |
| `audit_time` | timestamp |  | Audit Time |
| `process_time` | int |  | Process Time for Audit Completion |
| `risk_tier` | varchar(32) |  | Risk Level for Merchant |
| `memo` | varchar(500) |  | Audit Memo |
| `created_time` | timestamp |  | Created Time |
| `last_updated_time` | timestamp | NOT NULL | Last Updated Time |
| `data_version` | bigint | NOT NULL | Data Version |
| `apply_reason` | varchar(500) |  | Reason for the application |
| `from_mcc` | varchar(32) |  | old Mcc being update to |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
