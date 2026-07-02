---
id: tbl_credit_t_cs_repay_receipt
object_type: Table
name: 线下还款凭证表 (t_cs_repay_receipt)
aliases: [t_cs_repay_receipt, credit.t_cs_repay_receipt]
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

# 线下还款凭证表 (t_cs_repay_receipt)

## 用途
物理表 `credit.t_cs_repay_receipt`,主键 `id`。线下还款凭证表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | smallint(5) | 凭证状态 |
| `user_id` | varchar(50) | 用户ID · 可空 |
| `bank_name` | varchar(20) | 银行名 · 可空 |
| `mobile` | varchar(30) | 手机号 · 可空 |
| `bank_num` | varchar(50) | 银行卡号 · 可空 |
| `order_no` | varchar(50) | 订单 · 可空 |
| `amount` | decimal(15, 2) | 金额 |
| `receipt01_url` | varchar(500) | 图片地址 |
| `receipt02_url` | varchar(500) | 图片地址 |
| `receipt_date` | date | 还款日期 · 可空 |
| `product` | tinyint(5) | 产品码 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `holder_name` | varchar(100) | 持卡人姓名 · 可空 |
| `bank_channel` | varchar(30) | bank channel · 可空 |
| `own_account` | tinyint(5) | 1:self  0:others · 可空 |
| `reference_no` | varchar(50) | reference no · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
