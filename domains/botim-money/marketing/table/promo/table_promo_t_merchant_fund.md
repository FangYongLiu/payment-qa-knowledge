---
id: tbl_promo_t_merchant_fund
object_type: Table
name: Merchant found channel information (t_merchant_fund)
aliases: [t_merchant_fund, promo.t_merchant_fund]
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

# Merchant found channel information (t_merchant_fund)

## 用途
物理表 `promo.t_merchant_fund`,主键 `id`。Merchant found channel information。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `merchant_id` | varchar(32) | the found owner |
| `fund_channel` | varchar(50) | Found Channel, e.g., PayBy |
| `fund_account` | varchar(50) | the found account which is used to pay rewards to customers |
| `balance` | decimal(14, 2) | the balance of the account · 可空 |
| `status` | varchar(10) | the merchant found status: Active, Inactive |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `u_merchant_found_name`:merchant_id, fund_channel, fund_account (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
