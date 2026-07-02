---
id: tbl_promo_t_tool_promo_code_rule
object_type: Table
name: PromoCode Rules (t_tool_promo_code_rule)
aliases: [t_tool_promo_code_rule, promo.t_tool_promo_code_rule]
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

# PromoCode Rules (t_tool_promo_code_rule)

## 用途
物理表 `promo.t_tool_promo_code_rule`,主键 `id`。PromoCode Rules。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `promo_code_id` | varchar(32) | 待补 |
| `name` | varchar(50) | rule name |
| `rule` | varchar(2000) | rule json object, one rule - one object |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
