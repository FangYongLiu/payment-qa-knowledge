---
id: tbl_kyc_tm_message_event
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- notify
- tm_message_event
subdomain: notify
module: null
sensitivity: normal
name: 通知事件表(tm_message_event)
aliases:
- tm_message_event
related_services:
- svc_kyc
related_scenarios: []
---

# 通知事件表(tm_message_event)

## 用途
**通知事件规则表**:事件类型→匹配规则→通知策略→内容配置(`config_id`→tm_message_config) 的映射,按 partner 维度。配置类。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `event_type` | varchar(32) | NOT NULL | 事件类型 |
| `message_rule` | varchar(125) | NOT NULL | 匹配规则 |
| `message_strategy` | varchar(255) | NOT NULL | 通知策略 |
| `notify_method` | varchar(5) |  | 消息发送方式 |
| `status` | varchar(5) | NOT NULL | 状态（是否有效） |
| `config_id` | bigint | NOT NULL | 内容配置ID |
| `partner_id` | varchar(25) | 默认 'default' | 平台ID |
| `operators` | varchar(125) |  | Operators |
| `operator_type` | varchar(55) |  | Operator type |
| `extension` | varchar(255) |  | 拓展字段 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- `config_id` 指向有效的 tm_message_config。
- `message_rule`/`message_strategy` 命中即触发 tm_notify_record。
- 按 partner_id 隔离。
