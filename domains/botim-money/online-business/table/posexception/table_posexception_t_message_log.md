---
id: tbl_posexception_t_message_log
object_type: Table
name: 消息日志表 (t_message_log)
aliases: [t_message_log, posexception.t_message_log]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: posexception schema DDL
tags: [online-business, posexception]
sensitivity: normal
related_services: []
---

# 消息日志表 (t_message_log)

## 用途
物理表 `posexception.t_message_log`,主键 `id`。消息日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 订单号 |
| `order_id` | bigint | orderId |
| `response_message_key` | varchar(64) | responseMessageKey · 可空 |
| `request_message_key` | varchar(64) | requestMessageKey · 可空 |
| `request_no` | varchar(128) | 商户订单号 |
| `message_log_type` | varchar(32) | messageLogType |
| `created_time` | timestamp(3) | 创建时间 |
| `request_time` | timestamp(3) | requestTime |
| `expired_time` | timestamp(3) | expiredTime |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_ao_ct`:created_time
- `i_ao_lut`:expired_time
- `i_oi`:order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
