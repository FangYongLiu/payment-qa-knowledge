---
id: tbl_mns_t_notify_redo
object_type: Table
name: 消息重试 (t_notify_redo)
aliases: [t_notify_redo, mns.t_notify_redo]
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

# 消息重试 (t_notify_redo)

## 用途
物理表 `mns.t_notify_redo`,主键 `id`。消息重试。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(16) | 主键id |
| `msg_id` | bigint(18) | 消息id |
| `retried_times` | int(5) | 重试次数 |
| `max_retry_times` | int(5) | 最大重试次数 |
| `status` | varchar(1) | i-初始 s-成功 f-失败 |
| `ip_addr` | varchar(32) | ip地址 · 可空 |
| `retry_memo` | varchar(256) | 重试备注 · 可空 |
| `gmt_next_notify` | timestamp | 下次通知时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(256) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_msg_id`:msg_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
