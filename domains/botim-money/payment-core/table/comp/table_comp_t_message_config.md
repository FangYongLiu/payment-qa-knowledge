---
id: tbl_comp_t_message_config
object_type: Table
name: 消息发送配置 (t_message_config)
aliases: [t_message_config, comp.t_message_config]
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

# 消息发送配置 (t_message_config)

## 用途
物理表 `comp.t_message_config`,主键 `id`。消息发送配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `event_type` | varchar(16) | 事件类型 |
| `notify_type` | varchar(16) | 通知类型 sms,msg |
| `partner_id` | varchar(32) | 通知平台 · 可空 |
| `content_mode` | varchar(32) | 内容模式 mns,default |
| `match_rule` | varchar(32) | 匹配规则 · 可空 |
| `template_content_id` | varchar(32) | 内容模板id |
| `enable_flag` | varchar(32) | 有效标记 |
| `extension` | varchar(32) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
