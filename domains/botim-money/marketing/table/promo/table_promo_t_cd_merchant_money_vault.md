---
id: tbl_promo_t_cd_merchant_money_vault
object_type: Table
name: merchant vault (t_cd_merchant_money_vault)
aliases: [t_cd_merchant_money_vault, promo.t_cd_merchant_money_vault]
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

# merchant vault (t_cd_merchant_money_vault)

## 用途
物理表 `promo.t_cd_merchant_money_vault`,主键 `id`。merchant vault。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `owner_id` | char(32) | owner id who owns the money vault |
| `channel` | varchar(255) | channel of the money vault |
| `channel_account` | varchar(255) | account of the channel of the money vault |
| `balance` | decimal(19, 4) | balance of owner |
| `freeze_balance` | decimal(19, 4) | freeze balance of the owner |
| `currency` | char(3) | currency of the money vault |
| `status` | char(8) | Status: Active|Inactive |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |
| `is_default` | tinyint(1) | is default |

## 主键 / 索引
- 主键:`id`
- `idx_owner_id`:owner_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
