---
id: tbl_mss_t_activity_tool_relation
object_type: Table
name: 活动与工具关联关系 (t_activity_tool_relation)
aliases: [t_activity_tool_relation, mss.t_activity_tool_relation]
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

# 活动与工具关联关系 (t_activity_tool_relation)

## 用途
物理表 `mss.t_activity_tool_relation`,主键 `relation_id`。活动与工具关联关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | int | 主键id · 可空 |
| `activity_code` | varchar(64) | 活动id · 可空 |
| `tool_id` | int | 工具id · 可空 |
| `status` | char | 状态 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`relation_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
