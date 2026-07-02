---
id: tbl_creditinvoice_t_deduct_income
object_type: Table
name: 发票收入抵扣记录表 (t_deduct_income)
aliases: [t_deduct_income, creditinvoice.t_deduct_income]
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

# 发票收入抵扣记录表 (t_deduct_income)

## 用途
物理表 `creditinvoice.t_deduct_income`,主键 `id`。发票收入抵扣记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `product_code` | varchar(64) | 产品码 |
| `ref_busi_no` | varchar(64) | 引起收入抵扣的业务订单号,deduct_type=2时:被退票的借款订单的order_no,deduct_type=4时:减免记录id,deduct_type=6时:优惠券记录id,deduct_type=8时:引起退票的退票订单id |
| `deduct_type` | smallint(4) | 抵扣类型：2:退票,4:减免抵扣,6:优惠券抵扣,8:还款退回 |
| `income_id` | int | 对应t_cs_income表的ID |
| `total_deduct_amount` | decimal(15, 4) | 抵扣金额 |
| `deduct_instalment_fee` | decimal(15, 4) | total_deduct_amount中有多少是抵扣利息 · 可空 |
| `deduct_latepayment_fee` | decimal(15, 4) | total_deduct_amount中有多少是抵扣罚息 · 可空 |
| `deduct_process_fee` | decimal(15, 4) | total_deduct_amount中有多少是抵扣扣头息或展期费或提前结清手续费 · 可空 |
| `status` | smallint(4) | 1：正常，-1 删除 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `repay_reduct_idx`:income_id, ref_busi_no, deduct_type, product_code (UNIQUE)
- `ix_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
