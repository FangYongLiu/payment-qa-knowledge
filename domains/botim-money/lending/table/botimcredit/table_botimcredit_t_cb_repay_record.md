---
id: tbl_botimcredit_t_cb_repay_record
object_type: Table
name: 还款记录 (t_cb_repay_record)
aliases: [t_cb_repay_record, botimcredit.t_cb_repay_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# 还款记录 (t_cb_repay_record)

## 用途
物理表 `botimcredit.t_cb_repay_record`,主键 `id`。还款记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 待补 · 可空 |
| `order_no` | varchar(64) | 订单ID |
| `repay_amount` | decimal(15, 2) | 还款金额 |
| `repay_way` | smallint | 还款方式 |
| `repay_time` | timestamp | 三方入帐时间 |
| `status` | smallint | 还款状态 0 还款中， 1还款成功 -1还款失败 |
| `payment_no` | bigint | 支付凭证号 · 可空 |
| `repay_channel` | varchar(64) | 还款渠道 · 可空 |
| `repay_no` | varchar(64) | 还款订单号 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `user_id` | varchar(20) | 用户ID · 可空 |
| `partner_id` | varchar(20) | 渠道 |
| `referenceNo` | varchar(64) | 线下还款凭证 · 可空 |
| `referenceNo1` | varchar(64) | 线下还款凭证 · 可空 |
| `reference_no` | varchar(64) | 线下还款凭证 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_payment_no`:payment_no
- `idx_repay_record_reference_no`:referenceNo

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
