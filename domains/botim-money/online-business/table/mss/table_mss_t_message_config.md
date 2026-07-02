---
id: tbl_mss_t_message_config
object_type: Table
name: 消息配置 (t_message_config)
aliases: [t_message_config, mss.t_message_config]
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

# 消息配置 (t_message_config)

## 用途
物理表 `mss.t_message_config`,主键 `id`。消息配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `event_type` | varchar(128) | 事件类型 |
| `notify_type` | varchar(16) | 通知类型 公众号，短信 |
| `match_rule` | varchar(64) | 匹配规则 |
| `notify_strategy` | varchar(64) | 通知策略 · 可空 |
| `notify_strategy_type` | varchar(16) | 通知策略类型 · 可空 |
| `status` | char | 状态 |
| `content_id` | int | 通知内容id · 可空 |
| `extension` | varchar(64) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
