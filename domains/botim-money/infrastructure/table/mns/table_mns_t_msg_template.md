---
id: tbl_mns_t_msg_template
object_type: Table
name: 消息模板 (t_msg_template)
aliases: [t_msg_template, mns.t_msg_template]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mns schema DDL
tags: [infrastructure, mns]
sensitivity: normal
related_services: []
---

# 消息模板 (t_msg_template)

## 用途
物理表 `mns.t_msg_template`,主键 `id`。消息模板。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `template_no` | varchar(50) | 渠道名 |
| `msg_type` | varchar(1) | 短信回执id |
| `subject` | varchar(256) | 链接信息 · 可空 |
| `partner_id` | varchar(22) | 平台id · 可空 |
| `msg_content` | text | 链接信息 |
| `app_id` | varchar(20) | 应用标示 · 可空 |
| `title` | varchar(64) | 标题 · 可空 |
| `gmt_notify` | timestamp | 通知时间，若是实时发送，该字段会小于等于当前时间 |
| `gmt_effect` | timestamp | 生效时间 |
| `gmt_expired` | timestamp | 时效时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |
| `lang` | varchar(3) | 语言 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
