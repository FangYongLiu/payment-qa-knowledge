---
id: tbl_mss_t_message_content
object_type: Table
name: 消息内容 (t_message_content)
aliases: [t_message_content, mss.t_message_content]
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

# 消息内容 (t_message_content)

## 用途
物理表 `mss.t_message_content`,主键 `id`。消息内容。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `message_config_id` | int | 通知配置id |
| `notify_type` | varchar(32) | 通知类型 |
| `title` | varchar(64) | 标题 |
| `sub_title` | varchar(64) | 副标题 · 可空 |
| `digest` | varchar(512) | 摘要 · 可空 |
| `content` | varchar(512) | 内容文案 · 可空 |
| `link_url` | varchar(255) | 链接 · 可空 |
| `notify_target` | varchar(64) | 通知地址 · 可空 |
| `status` | char | 状态 |
| `extension` | varchar(64) | 扩展信息 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
