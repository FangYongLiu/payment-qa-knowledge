---
id: tbl_npss_t_bank_message
object_type: Table
name: 收到的uaeipp消息 (t_bank_message)
aliases: [t_bank_message, npss.t_bank_message]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 收到的uaeipp消息 (t_bank_message)

## 用途
物理表 `npss.t_bank_message`,主键 `message_id`。收到的uaeipp消息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `message_id` | bigint(17) | 消息id |
| `bank_msg_id` | varchar(32) | 消息id · 可空 |
| `message_type` | varchar(10) | 消息类型 |
| `message_content` | varchar(2048) | 消息内容 |
| `status` | char | 状态 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`message_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
