---
id: tbl_botimsnpl_t_sl_async_message
object_type: Table
name: local message table (t_sl_async_message)
aliases: [t_sl_async_message, botimsnpl.t_sl_async_message]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# local message table (t_sl_async_message)

## 用途
物理表 `botimsnpl.t_sl_async_message`,主键 `id`。local message table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `biz_type` | varchar(64) | business type, like, ORDER_ASYNC |
| `biz_no` | varchar(64) | business no |
| `msg_type` | varchar(64) | AsyncOperationType |
| `payload` | varchar(1024) | AsyncOperation JSON |
| `status` | tinyint | 0=pending 1=finished 2=dead |
| `retry_count` | int | retry count |
| `next_retry_time` | datetime | next retry time |
| `last_error` | varchar(256) | last error description · 可空 |
| `sent_time` | datetime | send time · 可空 |
| `created_time` | datetime | created time |
| `last_modified` | datetime | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_biz_no`:biz_no
- `idx_status_next_retry`:status, next_retry_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
