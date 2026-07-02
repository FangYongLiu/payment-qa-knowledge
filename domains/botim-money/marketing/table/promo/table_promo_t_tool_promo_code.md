---
id: tbl_promo_t_tool_promo_code
object_type: Table
name: Tools - Promo Code (t_tool_promo_code)
aliases: [t_tool_promo_code, promo.t_tool_promo_code]
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

# Tools - Promo Code (t_tool_promo_code)

## 用途
物理表 `promo.t_tool_promo_code`,主键 `id`。Tools - Promo Code。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `batch_id` | varchar(32) | the promo code creation batch |
| `merchant_id` | varchar(32) | 待补 |
| `campaign_id` | varchar(32) | 待补 |
| `code_type` | varchar(20) | code type enum: Unique, SameConstruct, DiffConstruct |
| `code` | varchar(40) | 待补 |
| `status` | varchar(20) | promo code status enum: Active, Inactive |
| `available_since` | timestamp | 待补 |
| `expired_since` | timestamp | 待补 |
| `sort` | int | 待补 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
