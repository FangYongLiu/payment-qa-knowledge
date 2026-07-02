---
id: tbl_mns_t_channel_config
object_type: Table
name: 消息发送渠道配置信息 (t_channel_config)
aliases: [t_channel_config, mns.t_channel_config]
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

# 消息发送渠道配置信息 (t_channel_config)

## 用途
物理表 `mns.t_channel_config`,主键 `id`。消息发送渠道配置信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `channel_id` | bigint(16) | 发送渠道 |
| `msg_type` | varchar(1) | s-短信  m-电子邮件   p-新浪站内信 · 可空 |
| `description` | varchar(256) | 描述 · 可空 |
| `config_key` | varchar(64) | 配置键 |
| `config_value` | varchar(512) | 配置值 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_channel_config`:channel_id, msg_type

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
