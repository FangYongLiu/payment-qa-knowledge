---
id: tbl_tldservice_t_tld_notify_order
object_type: Table
name: tld notify order (t_tld_notify_order)
aliases: [t_tld_notify_order, tldservice.t_tld_notify_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tldservice schema DDL
tags: [marketing, tldservice]
sensitivity: normal
related_services: []
---

# tld notify order (t_tld_notify_order)

## 用途
物理表 `tldservice.t_tld_notify_order`,主键 `id`。tld notify order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `order_type` | varchar(32) | orderType |
| `business_order_id` | varchar(32) | businessOrderId |
| `status` | varchar(32) | status |
| `retry_count` | int | retryCount |
| `max_retry_count` | int | maxRetryCount |
| `next_retry_time` | timestamp(3) | nextRetryTime |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | udpated_time |
| `data_version` | bigint | data version |

## 主键 / 索引
- 主键:`id`
- `uk_tno_ob`:order_type, business_order_id (UNIQUE)
- `i_tno_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
