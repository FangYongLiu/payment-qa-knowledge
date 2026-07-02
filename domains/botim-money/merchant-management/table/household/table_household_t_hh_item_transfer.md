---
id: tbl_household_t_hh_item_transfer
object_type: Table
name: household transfer (t_hh_item_transfer)
aliases: [t_hh_item_transfer, household.t_hh_item_transfer]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# household transfer (t_hh_item_transfer)

## 用途
物理表 `household.t_hh_item_transfer`,主键 `id`。household transfer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `beneficiary_id` | varchar(32) | beneficiary id |
| `amount` | decimal(19, 4) | amount |
| `currency` | char(3) | currency (default AED) |
| `repeat_date` | int | repeat date |
| `pay_short_code` | varchar(32) | pay short code |
| `pay_type` | varchar(64) | pay type · 可空 |
| `card_brand` | varchar(32) | card brand · 可空 |
| `card_type` | varchar(32) | card type |
| `last_four` | char(4) | last four |
| `status` | char(8) | enum:Draft|Official|Deleted |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_repeat_date`:repeat_date
- `idx_wallet_owner_id`:wallet_owner_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
