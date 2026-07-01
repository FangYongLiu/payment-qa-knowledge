---
id: tbl_merchant_t_merchant_payment_gateway_info
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
- t_merchant_payment_gateway_info
subdomain: merchant
module: null
sensitivity: normal
name: 商户支付网关信息(t_merchant_payment_gateway_info)
aliases:
- t_merchant_payment_gateway_info
related_services:
- svc_merchant
related_scenarios: []
---
# 商户支付网关信息(t_merchant_payment_gateway_info)

## 用途
商户支付网关信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC |  |
| `merchant_creation_id` | bigint | NOT NULL | Merchant Creation Id |
| `delivery_methods_specified` | varchar(3) | NOT NULL | Delivery Methods Specified (yes/no) |
| `delivery_methods_url` | varchar(255) | NOT NULL | Delivery Methods URL |
| `refund_policies_stated` | varchar(3) | NOT NULL | Refund Policies Stated (yes/no) |
| `privacy_policy_exists` | varchar(3) | NOT NULL | Privacy Policy Exists (yes/no) |
| `payment_logos_displayed` | varchar(3) | NOT NULL | Payment Logos Displayed (yes/no) |
| `payment_logos_url` | varchar(255) | NOT NULL | Payment Logos URL |
| `tls_ssl_certificate` | varchar(3) | NOT NULL | TLS/SSL Certificate (yes/no) |
| `domain_ownership_proof` | varchar(3) | NOT NULL | Domain Ownership Proof (yes/no) |
| `age_restrictions` | varchar(3) | NOT NULL | Age Restrictions (yes/no) |
| `collects_cardholder_data` | varchar(3) | NOT NULL | Collects Cardholder Data (yes/no) |
| `pci_dss_cert_path` | varchar(255) | NOT NULL | PCI DSS Certificate Path |
| `customer_due_diligence` | varchar(3) | NOT NULL | Customer Due Diligence (yes/no) |
| `due_diligence_description` | varchar(255) | NOT NULL | Due Diligence Description |
| `fraud_prevention_measures` | varchar(255) |  | Fraud Prevention Measures Description |
| `risk_monitoring_tools` | varchar(255) |  | Risk Monitoring Tools Description |
| `chargeback_management` | varchar(255) |  | Chargeback Management Description |
| `created_time` | timestamp | 默认 CURRENT_TIMESTAMP | Created At Time |
| `last_updated_time` | timestamp | 默认 CURRENT_TIMESTAMP | Last Updated Time |
| `refund_policies_url` | varchar(255) |  | Refund Policies Url |
| `privacy_policy_url` | varchar(255) |  | Privacy Policy Url |
| `home_page_url` | varchar(255) |  | Home Page Url |
| `payment_page_url` | varchar(255) |  | Payment Page Url |
| `data_version` | bigint | 默认 1 | Data version for concurrency control |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_creation_id` (merchant_creation_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
