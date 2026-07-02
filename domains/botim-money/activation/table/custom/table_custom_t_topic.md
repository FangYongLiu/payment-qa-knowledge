---
id: tbl_custom_t_topic
object_type: Table
name: 主题表 (t_topic)
aliases: [t_topic, custom.t_topic]
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

# 主题表 (t_topic)

## 用途
物理表 `custom.t_topic`,主键 `id`。主题表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `topic_name` | varchar(50) | 主题名称 |
| `flow_model` | varchar(16) | 主题流程模式 · 可空 |
| `status` | varchar(1) | 状态（1：有效 0：失效） |
| `create_time` | timestamp | 创建时间 · 可空 |
| `modify_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
