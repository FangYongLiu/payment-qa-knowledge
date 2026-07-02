---
id: tbl_cashdesk_t_group_scheme_rel
object_type: Table
name: 商户组与策略方案关系表 (t_group_scheme_rel)
aliases: [t_group_scheme_rel, cashdesk.t_group_scheme_rel]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 商户组与策略方案关系表 (t_group_scheme_rel)

## 用途
物理表 `cashdesk.t_group_scheme_rel`,主键 `id`。商户组与策略方案关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `group_id` | bigint | 组id |
| `product_code` | bigint | 产品代码 |
| `scheme_code` | bigint | 方案代码 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
