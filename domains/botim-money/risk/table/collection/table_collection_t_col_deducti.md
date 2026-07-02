---
id: tbl_collection_t_col_deducti
object_type: Table
name: 还款抵扣表 (t_col_deducti)
aliases: [t_col_deducti, collection.t_col_deducti]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 还款抵扣表 (t_col_deducti)

## 用途
物理表 `collection.t_col_deducti`,主键 `id`。还款抵扣表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(64) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(64) | 更新人员 · 可空 |
| `deducti_id` | varchar(64) | 发起抵扣的还款id |
| `repay_id` | varchar(64) | 被扣减的还款id |
| `total_reduct_capital` | decimal(19, 2) | 抵扣的总本金 |
| `deduct_instalment_fee` | decimal(19, 2) | 扣减的手续费 |
| `deduct_latepayment_fee` | decimal(19, 2) | 扣减的罚息 |

## 主键 / 索引
- 主键:`id`
- `idx_deducti_id`:deducti_id
- `idx_repay_id`:repay_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
