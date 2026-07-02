---
id: tbl_mchtsettle_t_merchant_summary
object_type: Table
name: merchant summary (t_merchant_summary)
aliases: [t_merchant_summary, mchtsettle.t_merchant_summary]
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

# merchant summary (t_merchant_summary)

## 用途
物理表 `mchtsettle.t_merchant_summary`,主键 `id`。merchant summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `batch_id` | bigint | batch id |
| `merchant_mid` | varchar(50) | merchant mid |
| `count` | bigint | count |
| `settlement_time` | timestamp(3) | settlement time |
| `settlement_job_id` | bigint | settlement job_id · 可空 |
| `status` | varchar(20) | status |
| `clearing_amount` | decimal(19, 4) | clearing amount |
| `clearing_currency` | char(3) | clearing currency |
| `fee_amount` | decimal(19, 4) | fee amount |
| `fee_currency` | char(3) | fee currency |
| `net_amount` | decimal(19, 4) | net amount |
| `net_currency` | char(3) | net currency |
| `vat_amount` | decimal(19, 4) | vat amount |
| `vat_currency` | char(3) | vat currency |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | last updated time |
| `data_version` | bigint | data_version |
| `safe_chunk_id` | bigint | safe_chunk_id · 可空 |
| `risky_chunk_id` | bigint | risky_chunk_id · 可空 |
| `logic_version` | int | logic_version · 可空 |
| `job_version` | int | job_version · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_ms_mid`:batch_id, merchant_mid (UNIQUE)
- `i_ms_job`:settlement_job_id
- `i_ms_stl_time`:settlement_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
