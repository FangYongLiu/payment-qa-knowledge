---
id: tbl_comp_t_message_content
object_type: Table
name: 消息内容 (t_message_content)
aliases: [t_message_content, comp.t_message_content]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: comp schema DDL
tags: [payment-core, comp]
sensitivity: normal
related_services: []
---

# 消息内容 (t_message_content)

## 用途
物理表 `comp.t_message_content`,主键 `id`。消息内容。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id |
| `title` | varchar(255) | 标题 |
| `sub_title` | varchar(255) | 副标题 · 可空 |
| `digest` | varchar(255) | 摘要 · 可空 |
| `content` | varchar(1024) | 内容文案 |
| `link_url` | varchar(255) | 链接 · 可空 |
| `resource_url` | varchar(255) | 资源地址 · 可空 |
| `notify_addr` | varchar(255) | 通知地址 · 可空 |
| `extension` | varchar(128) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
