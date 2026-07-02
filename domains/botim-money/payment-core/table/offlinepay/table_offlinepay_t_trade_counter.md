---
id: tbl_offlinepay_t_trade_counter
object_type: Table
name: Trace Counter (t_trade_counter)
aliases: [t_trade_counter, offlinepay.t_trade_counter]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# Trace Counter (t_trade_counter)

## 用途
物理表 `offlinepay.t_trade_counter`,主键 `id`。Trace Counter。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `trade_date` | varchar(6) | ymmdd |
| `count` | bigint | count · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`id`
- `i_tc_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
