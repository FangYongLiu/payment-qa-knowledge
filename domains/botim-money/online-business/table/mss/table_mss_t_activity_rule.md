---
id: tbl_mss_t_activity_rule
object_type: Table
name: 活动规则 活动专有规则 (t_activity_rule)
aliases: [t_activity_rule, mss.t_activity_rule]
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

# 活动规则 活动专有规则 (t_activity_rule)

## 用途
物理表 `mss.t_activity_rule`,主键 `rule_id`。活动规则 活动专有规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rule_id` | int | 主键id · 可空 |
| `activity_code` | varchar(64) | 活动id |
| `rule_type` | varchar(16) | 规则类型 |
| `rule_code` | varchar(32) | 规则code |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
