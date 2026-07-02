---
id: tbl_promo_t_cd_rewa_cash_desk_applied
object_type: Table
name: cash desk applied reward (t_cd_rewa_cash_desk_applied)
aliases: [t_cd_rewa_cash_desk_applied, promo.t_cd_rewa_cash_desk_applied]
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

# cash desk applied reward (t_cd_rewa_cash_desk_applied)

## 用途
物理表 `promo.t_cd_rewa_cash_desk_applied`,主键 `id`。cash desk applied reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `applied_reward_id` | char(32) | applied reward id |
| `order_no` | varchar(20) | order no |
| `status` | char(6) | enum:Lock|Unlock|Redeem |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_applied_reward_id`:applied_reward_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
