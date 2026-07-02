---
id: tbl_ppcenter_t_dcc_markup_apply
object_type: Table
name: DCC markup rate change audit (t_dcc_markup_apply)
aliases: [t_dcc_markup_apply, ppcenter.t_dcc_markup_apply]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppcenter schema DDL
tags: [activation, ppcenter]
sensitivity: normal
related_services: []
---

# DCC markup rate change audit (t_dcc_markup_apply)

## 用途
物理表 `ppcenter.t_dcc_markup_apply`,主键 `id`。DCC markup rate change audit。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `apply_id` | bigint | FK to product apply order · 可空 |
| `original_rate` | decimal(10, 6) | Original markup rate |
| `new_rate` | decimal(10, 6) | New markup rate |
| `gmt_create` | timestamp | Markup apply create date |
| `gmt_modify` | timestamp | Markup apply update date |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
