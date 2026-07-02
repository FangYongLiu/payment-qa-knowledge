---
id: tbl_mchtsettle_t_settle_step
object_type: Table
name: merchant settle step (t_settle_step)
aliases: [t_settle_step, mchtsettle.t_settle_step]
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

# merchant settle step (t_settle_step)

## 用途
物理表 `mchtsettle.t_settle_step`,主键 `id`。merchant settle step。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `status` | varchar(16) | status |
| `freeze` | varchar(4) | freeze |
| `usage` | varchar(4) | usage |
| `change_amount` | decimal(19, 4) | change_amount |
| `change_amount_currency` | char(3) | change_amount_currency |
| `end_amount` | decimal(19, 4) | end_amount · 可空 |
| `end_amount_currency` | char(3) | end_amount_currency · 可空 |
| `frozen_amount` | decimal(19, 4) | frozen_amount · 可空 |
| `frozen_amount_currency` | char(3) | frozen_amount_currency · 可空 |
| `merged_amount` | decimal(19, 4) | merged_amount · 可空 |
| `merged_amount_currency` | char(3) | merged_amount_currency · 可空 |
| `settled_amount` | decimal(19, 4) | settled_amount · 可空 |
| `settled_amount_currency` | char(3) | settled_amount_currency · 可空 |
| `start_amount` | decimal(19, 4) | start_amount |
| `start_amount_currency` | char(3) | start_amount_currency |
| `fee_amount` | decimal(19, 4) | fee_amount |
| `fee_amount_currency` | char(3) | fee_currency |
| `net_amount` | decimal(19, 4) | net_amount |
| `net_amount_currency` | char(3) | net_currency |
| `vat_amount` | decimal(19, 4) | vat_amount |
| `vat_amount_currency` | char(3) | vat_currency |
| `deduct_amount` | decimal(19, 4) | deduct_amount · 可空 |
| `deduct_amount_currency` | char(3) | deduct_currency · 可空 |
| `deducted_amount` | decimal(19, 4) | deducted_amount · 可空 |
| `deducted_amount_currency` | char(3) | deducted_currency · 可空 |
| `settled_time` | timestamp(3) | settleTime · 可空 |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `created_time` | timestamp(3) | created_time |
| `data_version` | bigint | data_version |
| `frozen_voucher_no` | bigint | frozen_voucher_no · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_ss_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
