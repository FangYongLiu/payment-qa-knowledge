---
id: tbl_router_t_channel_inst_relation
object_type: Table
name: 渠道机构关系表 (t_channel_inst_relation)
aliases: [t_channel_inst_relation, router.t_channel_inst_relation]
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

# 渠道机构关系表 (t_channel_inst_relation)

## 用途
物理表 `router.t_channel_inst_relation`,主键 `relation_id`。渠道机构关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | int | 主键 · 可空 |
| `channel_code` | varchar(32) | 渠道编号 · 可空 |
| `inst_code` | varchar(32) | 目标机构 · 可空 |

## 主键 / 索引
- 主键:`relation_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
