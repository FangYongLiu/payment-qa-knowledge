---
id: tbl_comp_t_notify_message
object_type: Table
name: 补偿后发送消息 (t_notify_message)
aliases: [t_notify_message, comp.t_notify_message]
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

# 补偿后发送消息 (t_notify_message)

## 用途
物理表 `comp.t_notify_message`,主键 `id`。补偿后发送消息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `comp_order_no` | bigint | 补单订单号 |
| `member_id` | varchar(32) | 通知用户 |
| `identity` | varchar(64) | 通知用户标识 |
| `partner_id` | varchar(32) | 通知平台 |
| `notify_type` | varchar(32) | 通知类型 短信，公众号 |
| `content_type` | varchar(32) | 内容标识 text,label |
| `lang_type` | varchar(32) | 语言 en,ar |
| `content` | varchar(512) | 通知内容 |
| `title` | varchar(255) | 标题 |
| `url` | varchar(255) | 点击跳转地址 · 可空 |
| `status` | varchar(32) | 状态 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
