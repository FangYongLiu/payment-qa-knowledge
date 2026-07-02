---
id: tbl_household_t_hh_contract
object_type: Table
name: household contract (t_hh_contract)
aliases: [t_hh_contract, household.t_hh_contract]
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

# household contract (t_hh_contract)

## 用途
物理表 `household.t_hh_contract`,主键 `id`。household contract。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `draft_id` | varchar(32) | draft id |
| `pay_short_code` | varchar(32) | pay short code |
| `pay_order_no` | varchar(64) | pay order no |
| `amount` | decimal(19, 4) | amount |
| `currency` | char(3) | currency (default AED) |
| `token` | varchar(255) | token |
| `kind` | varchar(8) | enum:Contract|identity |
| `status` | varchar(10) | enum:Inactive|Active|Processing|Deleted |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_pay_order_no`:pay_order_no
- `idx_wallet_owner_id`:wallet_owner_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
