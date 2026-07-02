---
id: tbl_rnpl_t_loan_product
object_type: Table
name: Credit Product Definition Table (t_loan_product)
aliases: [t_loan_product, rnpl.t_loan_product]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Credit Product Definition Table (t_loan_product)

## 用途
物理表 `rnpl.t_loan_product`,主键 `id`。Credit Product Definition Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `product_name` | varchar(128) | product name |
| `product_desc` | varchar(255) | product description · 可空 |
| `product_type` | varchar(16) | 1:RTR \n2: RNPL |
| `version` | smallint | version, when selecting a product, use the largest version of the same product_name |
| `inst_num` | smallint | number of product periods |
| `time_amount_per_inst` | smallint | number of time units per issue |
| `time_unit` | smallint | time unit: 1:day; 2:month |
| `processing_fee_rate` | decimal(10, 4) | deductible interest rate |
| `processing_fee_cap` | decimal(10, 2) | maximum Haircut Interest Amount · 可空 |
| `total_interest_rate` | decimal(10, 4) | total interest |
| `period_irr_rate` | decimal(10, 4) | period_irr_rate |
| `status` | smallint | Status: 1: normal; 0: deactivated |
| `use_condition` | varchar(1024) | conditions of use, in the format of a json string. Businesses that meet the corresponding conditions can use this product, currently known conditions: channels, scenarios (user direct application / rollover), user type (new user / renewing user), whether or not to increase the interest rate (isUpFee), the results of the experiment of placing an order (tag1/tag2/tag3) · 可空 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uniq_product_name_version`:product_name, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
