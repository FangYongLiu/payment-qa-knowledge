---
id: tbl_activity_t_condition
object_type: Table
name: 条件要求表，用于构建规则 (t_condition)
aliases: [t_condition, activity.t_condition]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# 条件要求表，用于构建规则 (t_condition)

## 用途
物理表 `activity.t_condition`,主键 `id`。条件要求表，用于构建规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | id · 可空 |
| `name` | varchar(128) | 名称 |
| `key` | varchar(128) | 条件的key |
| `operator` | varchar(16) | 判断表达式：==，!=,in，>,>=,<,<= |
| `value` | varchar(255) | 对于operator="in"的，要求是以逗号分隔 |

## 主键 / 索引
- 主键:`id`
- `ix_name`:name (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
