---
id: tbl_reconciliation_t_clear_fund_history_flow
object_type: Table
name: 对账清算历史流水 (t_clear_fund_history_flow)
aliases: [t_clear_fund_history_flow, reconciliation.t_clear_fund_history_flow]
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

# 对账清算历史流水 (t_clear_fund_history_flow)

## 用途
物理表 `reconciliation.t_clear_fund_history_flow`,主键 `history_id`。对账清算历史流水。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `history_id` | bigint | 待补 |
| `bill_batch_no` | varchar(32) | 对账批次号 · 可空 |
| `parse_batch_no` | varchar(32) | 解析批次号 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(8) | 业务类型 · 可空 |
| `payment_seq_no` | varchar(32) | 支付流水号 · 可空 |
| `clearing_order_no` | varchar(32) | 清算单号 · 可空 |
| `inst_order_no` | varchar(32) | 上送机构单号 · 可空 |
| `fund_date` | varchar(8) | 入账日期 · 可空 |
| `bill_date` | varchar(8) | 清算日期 · 可空 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 货币 币种 · 可空 |
| `bill_flag` | varchar(4) | 对账标记/状态 · 可空 |
| `gmt_fund_create` | timestamp | 入账流水创建时间 · 可空 |
| `gmt_bill_create` | timestamp | 清算流水创建时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `fund_extension` | varchar(512) | 入账流水扩展信息 · 可空 |
| `bill_extension` | varchar(512) | 清算流水扩展信息 · 可空 |

## 主键 / 索引
- 主键:`history_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
