---
id: tbl_creditinvoice_t_income
object_type: Table
name: 发票收入记录表 (t_income)
aliases: [t_income, creditinvoice.t_income]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# 发票收入记录表 (t_income)

## 用途
物理表 `creditinvoice.t_income`,主键 `id`。发票收入记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `product_code` | varchar(64) | 产品码 |
| `busi_entity_no` | varchar(64) | 收入所属业务主体的no |
| `income_type` | smallint(4) | 收入类型:1:放款扣头息收入,3:还款收入,5:展期收入,7:duedate收入 |
| `income_amount` | decimal(15, 4) | 收入金额=process_fee + instalment_fee + late_payment_fee |
| `process_fee` | decimal(15, 4) | income_type=1时扣头息,income_type=3时提前结清的费用,income_type=5时展期费 · 可空 |
| `instalment_fee` | decimal(15, 4) | income_type=3或income_type=7时有值,表示利息 · 可空 |
| `late_payment_fee` | decimal(15, 4) | income_type=3时有值，表示逾期费 · 可空 |
| `ref_busi_no` | varchar(64) | 带来收入的业务no:income_type=1时是t_cs_order表的order_no,income_type=3时是t_cs_repay_record表的id,income_type=5时是t_cs_order表的order_no,income_type=7时是t_cs_bill表的id |
| `status` | smallint(4) | 待补 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_no`:ref_busi_no, income_type, product_code (UNIQUE)
- `ix_bno`:busi_entity_no
- `ix_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
