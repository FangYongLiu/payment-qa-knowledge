---
id: tbl_collection_t_fc_call_event
object_type: Table
name: 呼叫事件表 (t_fc_call_event)
aliases: [t_fc_call_event, collection.t_fc_call_event]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 呼叫事件表 (t_fc_call_event)

## 用途
物理表 `collection.t_fc_call_event`,主键 `id`。呼叫事件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(50) | 修改人 · 可空 |
| `call_id` | varchar(20) | 呼叫id · 可空 |
| `caller` | varchar(30) | 主叫 |
| `callee` | varchar(30) | 被叫 |
| `send_event_id` | bigint(10) | 发送事件id |
| `round_uid` | varchar(40) | 轮次号 |
| `user_uid` | varchar(50) | 用户id |
| `bill_no` | varchar(50) | 账单id |
| `status` | tinyint(5) | 状态0待处理 1处理中 2完结 |
| `type` | tinyint(5) | 类型 1接通 2回拨 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_send_event_id`:send_event_id
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
