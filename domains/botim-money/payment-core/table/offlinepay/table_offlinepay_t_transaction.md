---
id: tbl_offlinepay_t_transaction
object_type: Table
name: Transaction (t_transaction)
aliases: [t_transaction, offlinepay.t_transaction]
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

# Transaction (t_transaction)

## 用途
物理表 `offlinepay.t_transaction`,主键 `global_id, reversal`。Transaction。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | golbal_id |
| `response_code` | varchar(32) | response_code · 可空 |
| `reversal` | char | reversal |
| `tx_time` | timestamp(3) | tx_time · 可空 |
| `tx_type` | varchar(16) | value:PURCHASE、REFUND · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id, reversal`
- `i_t_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
