---
id: tbl_eminstalment_t_credit_order
object_type: Table
name: 垫资授信申请表 (t_credit_order)
aliases: [t_credit_order, eminstalment.t_credit_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 垫资授信申请表 (t_credit_order)

## 用途
物理表 `eminstalment.t_credit_order`,主键 `id`。垫资授信申请表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `order_no` | varchar(64) | 授信申请订单唯一ID |
| `user_id` | varchar(20) | 用户ID |
| `product_id` | int | 申请分期产品id，对应t_product表的id |
| `status` | smallint(4) | 状态，1：审核中，-2审核拒绝，2：审核通过 |
| `goods_order_no` | varchar(64) | 关联商品订单id,对应表t_store_order表的id |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `audit_start_time` | timestamp | 提交审核时间 · 可空 |
| `audit_finish_time` | timestamp | 审核结束时间 · 可空 |
| `result_audit_record_id` | int | 给出最终授信结果的审核记录 · 可空 |
| `amount` | decimal(15, 2) | 商品金额 |
| `loan_amount` | decimal(15, 2) | 申请授信金额 |
| `downpayment_amount` | decimal(15, 2) | 首付金额，=amount-loan_amount |
| `total_profit` | decimal(15, 2) | 预计总利息 |
| `currency` | char(3) | 货币 |

## 主键 / 索引
- 主键:`id`
- `uk_gon`:goods_order_no (UNIQUE)
- `uk_on`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
