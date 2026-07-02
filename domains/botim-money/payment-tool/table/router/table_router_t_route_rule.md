---
id: tbl_router_t_route_rule
object_type: Table
name: 路由规则唯一索引 (t_route_rule)
aliases: [t_route_rule, router.t_route_rule]
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

# 路由规则唯一索引 (t_route_rule)

## 用途
物理表 `router.t_route_rule`,主键 `rule_id`。路由规则唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rule_id` | int(32) | 规则id · 可空 |
| `channel_code` | varchar(32) | 渠道编号 |
| `inst_code` | varchar(32) | 机构编号 · 可空 |
| `score` | int(12) | 评分 |
| `weight` | int(12) | 权重 |
| `memo` | varchar(32) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
