---
id: tbl_npss_t_merchant
object_type: Table
name: Merchant table with online info (t_merchant)
aliases: [t_merchant, npss.t_merchant]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# Merchant table with online info (t_merchant)

## 用途
物理表 `npss.t_merchant`,主键 `merchant_id`。Merchant table with online info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merchant_id` | varchar(20) | merchant id |
| `merchant_name` | varchar(256) | merchant name |
| `sub_name` | varchar(12) | sub name · 可空 |
| `vat_number` | varchar(64) | vat no |
| `mcc` | varchar(4) | mcc · 可空 |
| `mobile` | varchar(16) | mobile no |
| `merchant_tag` | varchar(7) | Merchant Tag · 可空 |
| `iban` | varchar(32) | iban  |
| `online_shop_id` | bigint | Aani generated, online shop id · 可空 |
| `online_cashdesk_id` | bigint | Aani generated, online cashdesk id · 可空 |
| `online_app_id` | varchar(64) | Online merchant appId · 可空 |
| `online_bank_account_id` | bigint | bank account id · 可空 |
| `status` | char | status |
| `memo` | varchar(128) | memo · 可空 |
| `extension` | varchar(255) | extension · 可空 |
| `gmt_create` | timestamp | create time |
| `gmt_modified` | timestamp | modify time · 可空 |

## 主键 / 索引
- 主键:`merchant_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
