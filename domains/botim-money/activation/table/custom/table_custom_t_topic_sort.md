---
id: tbl_custom_t_topic_sort
object_type: Table
name: 主题排序表 (t_topic_sort)
aliases: [t_topic_sort, custom.t_topic_sort]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: custom schema DDL
tags: [activation, custom]
sensitivity: normal
related_services: []
---

# 主题排序表 (t_topic_sort)

## 用途
物理表 `custom.t_topic_sort`,主键 `id`。主题排序表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `topic_id` | bigint(18) | 主题id |
| `sort_type` | varchar(16) | by_preference:按偏好 by_rule：按规则 |
| `item_type` | varchar(16) | 排序适用定制项类型 · 可空 |
| `sort_rule` | varchar(150) | 排序规则 · 可空 |
| `priority` | int(1) | 优先级（1-9） · 可空 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
