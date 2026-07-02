---
id: tbl_merchant_t_standard_pricing_package_mapping
object_type: Table
name: Standard Pricing Package Mappings (t_standard_pricing_package_mapping)
aliases: [t_standard_pricing_package_mapping, merchant.t_standard_pricing_package_mapping]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: merchant schema DDL
tags: [merchant-management, merchant]
sensitivity: normal
related_services: []
---

# Standard Pricing Package Mappings (t_standard_pricing_package_mapping)

## 用途
物理表 `merchant.t_standard_pricing_package_mapping`,主键 `id`。Standard Pricing Package Mappings。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `product_type` | varchar(32) | Product type: PAYMENT_GATEWAY, PAYMENT_LINK, POS |
| `pricing_group` | varchar(32) | Pricing group: CARD_PAYMENT, ADDITIONAL_FEE |
| `fee_category` | varchar(64) | Fee category: DOMESTIC_CARD, INTERNATIONAL_CARD, SETUP_FEE, etc. |
| `fee_display_name` | varchar(64) | Display name for frontend (e.g., "Domestic", "Setup fee") |
| `display_package_code` | varchar(64) | Single package code for fetching pricing from PPCenter API for display purposes · 可空 |
| `apply_package_code` | varchar(256) | Comma-separated package codes that will be actually applied to the merchant · 可空 |
| `package_name` | varchar(64) | Package name from PPCenter · 可空 |
| `fee_value` | varchar(64) | Fee value for display-only fees (e.g., "AED 1,500", "AED 100/month") · 可空 |
| `is_display_only` | tinyint(1) | 1 = Display only (not applied to PPCenter), 0 = Applied to PPCenter |
| `is_active` | tinyint(1) | 1 = Active, 0 = Inactive |
| `description` | varchar(128) | Description of this mapping · 可空 |
| `data_version` | bigint | Data version |
| `created_time` | timestamp | Created time |
| `last_updated_time` | timestamp | Last updated time |

## 主键 / 索引
- 主键:`id`
- `uk_product_fee`:product_type, fee_category (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
