---
id: tbl_reconciliation_t_bill_summary_detail
object_type: Table
name: 对账汇总明细 (t_bill_summary_detail)
aliases: [t_bill_summary_detail, reconciliation.t_bill_summary_detail]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 对账汇总明细 (t_bill_summary_detail)

## 用途
物理表 `reconciliation.t_bill_summary_detail`,主键 `id`。对账汇总明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `bill_batch_no` | varchar(32) | 对账批次编号 |
| `fund_channel_code` | varchar(32) | 渠道编号 |
| `payment_seq_no` | varchar(32) | 支付流水号 · 可空 |
| `clearing_order_no` | varchar(32) | 清算单号 · 可空 |
| `inst_order_no` | varchar(64) | 机构订单号 |
| `inst_seq_no` | varchar(32) | 渠道返回订单号 · 可空 |
| `bill_date` | varchar(8) | 对账日期 |
| `biz_type` | varchar(8) | 业务类型 I-充值 O-提现 B-退款 · 可空 |
| `tran_amount` | decimal(15, 2) | 我方交易金额 · 可空 |
| `currency` | varchar(3) | 货币 币种 · 可空 |
| `tran_date` | varchar(8) | 我方交易/入账时间 · 可空 |
| `channel_result_code` | varchar(32) | 渠道交易结果码 · 可空 |
| `channel_result_msg` | varchar(32) | 渠道交易结果信息 · 可空 |
| `channel_tran_amount` | decimal(15, 2) | 渠道交易金额 · 可空 |
| `channel_tran_date` | timestamp | 渠道交易日期 · 可空 |
| `bill_status` | varchar(8) | 对账状态；金额不一致 多账等等 · 可空 |
| `handle_flag` | varchar(8) | 是否进行处理 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |
| `message` | varchar(512) | 资金对账差错原因 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_channel_inst_biz`:fund_channel_code, inst_order_no, biz_type (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
