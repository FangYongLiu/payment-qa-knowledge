---
id: tbl_promo_t_rbac_feature
object_type: Table
name: features for rbac module (t_rbac_feature)
aliases: [t_rbac_feature, promo.t_rbac_feature]
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

# features for rbac module (t_rbac_feature)

## 用途
物理表 `promo.t_rbac_feature`,主键 `id`。features for rbac module。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `parent_id` | varchar(32) | 待补 · 可空 |
| `code` | varchar(50) | 待补 |
| `name` | varchar(100) | 待补 |
| `endpoint` | varchar(255) | 待补 · 可空 |
| `description` | varchar(200) | 待补 · 可空 |
| `status` | varchar(20) | Status: Active|Inactive |
| `creator` | varchar(32) | 待补 |
| `updater` | varchar(32) | 待补 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |
| `deleted` | tinyint(1) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
