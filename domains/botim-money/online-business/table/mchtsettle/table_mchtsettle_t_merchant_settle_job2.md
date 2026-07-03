---
id: tbl_mchtsettle_t_merchant_settle_job2
object_type: Table
name: merchant settle job2 (t_merchant_settle_job2)
aliases: [t_merchant_settle_job2, mchtsettle.t_merchant_settle_job2]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# merchant settle job2 (t_merchant_settle_job2)

## 用途
物理表 `mchtsettle.t_merchant_settle_job2`,主键 `id`。merchant settle job2。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `merchant_mid` | varchar(50) | merchantMid · 可空 |
| `prev_job_id` | bigint | prev_job_id · 可空 |
| `status` | varchar(32) | status · 可空 |
| `safe_id` | bigint | safe_id · 可空 |
| `risk_id` | bigint | risk_id · 可空 |
| `settle_time` | timestamp(3) | settleTime · 可空 |
| `scheduled_settle_time` | timestamp(3) | scheduledSettleTime |
| `start_amount` | decimal(19, 4) | startAmount |
| `start_currency` | char(3) | startCurrency |
| `end_amount` | decimal(19, 4) | end_amount · 可空 |
| `end_currency` | char(3) | end_currency · 可空 |
| `file_path` | varchar(65) | file_path · 可空 |
| `clearing_amount` | decimal(19, 4) | clearing_amount · 可空 |
| `clearing_amount_currency` | char(3) | clearing_amount_currency · 可空 |
| `fee_amount` | decimal(19, 4) | fee_amount · 可空 |
| `fee_amount_currency` | char(3) | fee_currency · 可空 |
| `net_amount` | decimal(19, 4) | net_amount · 可空 |
| `net_amount_currency` | char(3) | net_currency · 可空 |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `created_time` | timestamp(3) | created_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`id`
- `i_msj_ct`:created_time
- `i_msj_lut`:last_updated_time
- `i_msj_mid`:merchant_mid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
