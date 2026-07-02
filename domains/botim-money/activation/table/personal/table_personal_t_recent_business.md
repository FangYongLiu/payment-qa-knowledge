---
id: tbl_personal_t_recent_business
object_type: Table
name: 最近业务记录表 (t_recent_business)
aliases: [t_recent_business, personal.t_recent_business]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: personal schema DDL
tags: [activation, personal]
sensitivity: normal
related_services: []
---

# 最近业务记录表 (t_recent_business)

## 用途
物理表 `personal.t_recent_business`,主键 `id`。最近业务记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `payer_member_id` | varchar(32) | 付款人mid |
| `payer_partner_id` | varchar(32) | 付款人平台 |
| `bus_type` | varchar(20) | 业务类型(T_TO_FRIEND,T_TO_MOBILE,T_TO_BANK,C_T_TO_FRIEND,C_T_TO_MOBILE) |
| `payee_id` | varchar(20) | 收款id(member_id/account_id) |
| `payee_alias` | varchar(30) | 收款人别名 · 可空 |
| `payee_default_partner_id` | varchar(32) | 收款人默认通知平台 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `last_trade_time` | timestamp | 最近交易时间 |
| `last_trade_amount` | decimal(15, 4) | Last Transaction Amount · 可空 |
| `currency` | char(3) | Currency · 可空 |
| `gmt_created` | timestamp | 建立时间 · 可空 |
| `gmt_updated` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bus_type_payee_id`:bus_type, payee_id
- `idx_payer_mid_pid`:payer_member_id, payer_partner_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
