---
id: tbl_mss_t_event_rule
object_type: Table
name: 营销活动-限制规则关联表 (t_event_rule)
aliases: [t_event_rule, mss.t_event_rule]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 营销活动-限制规则关联表 (t_event_rule)

## 用途
物理表 `mss.t_event_rule`,主键 `event_id, rule_id`。营销活动-限制规则关联表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_id` | bigint | 活动id |
| `rule_id` | bigint | 规则id |

## 主键 / 索引
- 主键:`event_id, rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
