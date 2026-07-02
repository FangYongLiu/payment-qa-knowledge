---
id: tbl_sme_t_loan_product
object_type: Table
name: Credit product definition sheet (t_loan_product)
aliases: [t_loan_product, sme.t_loan_product]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Credit product definition sheet (t_loan_product)

## 用途
物理表 `sme.t_loan_product`,主键 `id`。Credit product definition sheet。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `target_user_type` | smallint | 待补 |
| `product_name` | varchar(128) | Product name |
| `product_desc` | varchar(255) | Product description · 可空 |
| `version` | smallint | 待补 |
| `When` | selecting | 待补 · 可空 |
| `inst_num` | smallint | The number of phases of the product |
| `time_amount_per_inst` | smallint | How many time units are there in each issue |
| `time_unit` | smallint | 待补 |
| `max_disburse_amount` | decimal(10, 2) | 待补 · 可空 |
| `processing_fee_rate` | decimal(10, 4) | Discount rate |
| `processing_fee_cap` | decimal(10, 2) | Maximum deduction amount · 可空 |
| `early_settlement_fee_rate` | decimal(10, 4) | Early clearance rate |
| `period_interest_rate` | decimal(10, 4) | irr interest rate for each period |
| `base_penalty` | decimal(10, 2) | The amount of the base penalty after a single bill is overdue |
| `penalty_rate` | decimal(10, 4) | Daily penalty rate |
| `penalty_cap` | decimal(10, 2) | Cap on a single bill penalty · 可空 |
| `tmp_oa` | decimal(10, 4) | The total penalty limit for an order shall not exceed the proportion of the order amount · 可空 |
| `min_loan_amount` | decimal(10, 2) | Minimum loan amount |
| `max_loan_amount` | decimal(10, 2) | Maximum loan amount |
| `status` | smallint | 待补 |
| `use_condition` | varchar(1024) | Conditions of use · 可空 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_id`:target_user_type, product_name, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
