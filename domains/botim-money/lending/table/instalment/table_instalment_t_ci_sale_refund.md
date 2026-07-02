---
id: tbl_instalment_t_ci_sale_refund
object_type: Table
name: 退款信息表 (t_ci_sale_refund)
aliases: [t_ci_sale_refund, instalment.t_ci_sale_refund]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 退款信息表 (t_ci_sale_refund)

## 用途
物理表 `instalment.t_ci_sale_refund`,主键 `id`。退款信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `updated_time` | timestamp | 修改日期 · 可空 |
| `status` | smallint(5) | 状态: 0 待还款 1  结清 |
| `type` | smallint(5) | 1 退商户款 2退首付款 3退还款 |
| `pay_mid` | varchar(64) | 用户id |
| `amount` | decimal(15, 2) | 退款金额 |
| `order_no` | varchar(64) | 关联订单id |
| `payment_no` | varchar(64) | 付款id |
| `global_no` | varchar(64) | 全局id |
| `credit_order_no` | varchar(64) | 对应借款id |
| `partner_id` | varchar(64) | 商户id |
| `refund_time` | timestamp | 退款时间 |

## 主键 / 索引
- 主键:`id`
- `idx_credit_order_no`:credit_order_no
- `idx_order_no`:order_no
- `idx_pay_mid`:pay_mid
- `idx_payment_no`:payment_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
