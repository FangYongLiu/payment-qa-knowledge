---
id: tbl_merchant_t_partner_merchant_pricing
object_type: Table
name: t_partner_merchant_pricing (t_partner_merchant_pricing)
aliases: [t_partner_merchant_pricing, merchant.t_partner_merchant_pricing]
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

# t_partner_merchant_pricing (t_partner_merchant_pricing)

## 用途
物理表 `merchant.t_partner_merchant_pricing`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `merchant_mid` | varchar(50) | Merchant MID |
| `partner_id` | varchar(64) | Partner ID · 可空 |
| `pricing_group` | varchar(40) | Pricing group: PAYMENT_METHODS, ALTERNATIVE_PAYMENT_METHODS, FEES_AND_CHARGES, OTHER_FEES · 可空 |
| `product_type` | varchar(40) | Product type: PAYMENT_GATEWAY, PAYMENT_LINK, POS · 可空 |
| `fee_category` | varchar(64) | Fee category: DOMESTIC_CARD, INTERNATIONAL_CARD, SETUP_FEE, etc. · 可空 |
| `card_type` | varchar(16) | Card pricing type: BLENDED, ITEMIZED · 可空 |
| `fee_name` | varchar(128) | Fee name · 可空 |
| `fix_rate` | decimal(10, 4) | Fixed charge rate · 可空 |
| `fix_charge` | decimal(12, 2) | Fixed charge amount · 可空 |
| `fee_value` | varchar(128) | Fee value for display (e.g., "AED 1,500", "AED 100/month") · 可空 |
| `package_code` | varchar(255) | Resolved PPC package code(s) for card lines · 可空 |
| `created_time` | timestamp | Created time |
| `last_updated_time` | timestamp | Last updated time |
| `data_version` | bigint | Data version |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
