---
id: tbl_credit_t_cs_deductible_income
object_type: Table
name: 减免本金收入抵扣记录表 (t_cs_deductible_income)
aliases: [t_cs_deductible_income, credit.t_cs_deductible_income]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 减免本金收入抵扣记录表 (t_cs_deductible_income)

## 用途
物理表 `credit.t_cs_deductible_income`,主键 `id`。减免本金收入抵扣记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `repay_record_id` | int | 对应t_cs_repay_record表的id,且 repay_channel 不等于以下值时：REDUCTION_PRINCIPAL、REDUCTION |
| `reduct_record_id` | int | 对应t_cs_repay_record表的id，且 repay_channel 为以下值时：REDUCTION_PRINCIPAL、REDUCTION |
| `total_reduct_capital` | decimal(15, 2) | 此次reduct_record_id减免的本金减免中有多少抵扣在了repay_record_id 中 |
| `deduct_instalment_fee` | decimal(15, 2) | total_reduct_capital中有多少是抵扣利息 |
| `deduct_latepayment_fee` | decimal(15, 2) | total_reduct_capital中有多少是抵扣罚息 |
| `status` | smallint(4) | 1：正常，-1 删除 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `repay_reduct_idx`:repay_record_id, reduct_record_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
