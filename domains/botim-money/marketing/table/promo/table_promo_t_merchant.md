---
id: tbl_promo_t_merchant
object_type: Table
name: Business Merchant (t_merchant)
aliases: [t_merchant, promo.t_merchant]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# Business Merchant (t_merchant)

## 用途
物理表 `promo.t_merchant`,主键 `id`。Business Merchant。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `code` | varchar(20) | 待补 |
| `name` | varchar(100) | the merchant name |
| `description` | varchar(300) | 待补 |
| `merchant_type` | varchar(20) | MerchantType: Root, General, VIP |
| `status` | varchar(10) | the merchant status: Active, Inactive |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `u_merchant_name`:name (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
