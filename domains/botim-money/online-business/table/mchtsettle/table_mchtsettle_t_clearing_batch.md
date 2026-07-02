---
id: tbl_mchtsettle_t_clearing_batch
object_type: Table
name: clearing batch (t_clearing_batch)
aliases: [t_clearing_batch, mchtsettle.t_clearing_batch]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: []
---

# clearing batch (t_clearing_batch)

## 用途
物理表 `mchtsettle.t_clearing_batch`,主键 `id`。clearing batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `process_start_date` | date | process_start_date · 可空 |
| `process_end_date` | date | process_end_date · 可空 |
| `status` | varchar(30) | clearing batch status · 可空 |
| `created_time` | timestamp(3) | created_time · 可空 |
| `last_updated_time` | timestamp(3) | last_updated_time · 可空 |
| `data_version` | bigint | data_version · 可空 |
| `batch_date` | date | batch_date |
| `logic_version` | int | logic version · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_batch_date`:batch_date (UNIQUE)
- `i_status`:status
- `i_tcb_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
