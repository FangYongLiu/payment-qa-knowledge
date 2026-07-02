---
id: tbl_router_t_order_no_rule
object_type: Table
name: 订单号规则表 (t_order_no_rule)
aliases: [t_order_no_rule, router.t_order_no_rule]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# 订单号规则表 (t_order_no_rule)

## 用途
物理表 `router.t_order_no_rule`,主键 `order_no_rule_id`。订单号规则表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_no_rule_id` | bigint(32) | 订单号规则id |
| `rule` | varchar(128) | 规则 · 可空 |
| `seq_name` | varchar(32) | 序列号 · 可空 |
| `memo` | varchar(32) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`order_no_rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
