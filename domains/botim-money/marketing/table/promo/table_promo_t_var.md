---
id: tbl_promo_t_var
object_type: Table
name: variables for a tool running instance (t_var)
aliases: [t_var, promo.t_var]
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

# variables for a tool running instance (t_var)

## 用途
物理表 `promo.t_var`,主键 `id`。variables for a tool running instance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `scope` | varchar(32) | 待补 |
| `name` | varchar(100) | 待补 |
| `value` | varchar(2000) | 待补 |
| `var_type` | varchar(20) | VarType: String, Int, Float, Bool, Json |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `u_campaign_var`:scope, name (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
