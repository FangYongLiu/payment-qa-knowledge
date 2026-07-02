---
id: tbl_reconciliation_t_fund_flow
object_type: Table
name: 中台推送入账流水 (t_fund_flow)
aliases: [t_fund_flow, reconciliation.t_fund_flow]
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

# 中台推送入账流水 (t_fund_flow)

## 用途
物理表 `reconciliation.t_fund_flow`,主键 `flow_id`。中台推送入账流水。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint | 待补 |
| `payment_seq_no` | varchar(32) | 支付流水号 · 可空 |
| `clearing_order_no` | varchar(32) | 清算单号 · 可空 |
| `fund_channel_code` | varchar(32) | 待补 |
| `inst_order_no` | varchar(64) | 机构订单号 |
| `biz_type` | varchar(8) | 业务类型 I/O/B |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 货币 币种 · 可空 |
| `fund_date` | varchar(8) | 入账日期 · 可空 |
| `bill_flag` | varchar(8) | 对账状态 I:初始化 S:成功 U:金额不等 U:金额不等 · 可空 |
| `bill_date` | varchar(8) | 对账日期 · 可空 |
| `status` | varchar(8) | 交易结果 终态 · 可空 |
| `operator` | varchar(32) | 操作者 · 可空 |
| `extension` | varchar(512) | 入账扩展信息 · 可空 |
| `gmt_create` | timestamp | 创建日期 |
| `gmt_modified` | timestamp | 更新日期 |
| `channel_type` | varchar(4) | 渠道类型: SC 供应商渠道 , FC 资金渠道 · 可空 |
| `fee_amount` | decimal(15, 4) | 手续费 · 可空 |
| `fee_currency` | char(3) | 手续费币种 · 可空 |
| `vat_amount` | decimal(15, 4) | 增值税 · 可空 |
| `vat_currency` | char(3) | 增值税币种 · 可空 |
| `paid_amount` | decimal(15, 4) | 支付金额 · 可空 |
| `paid_currency` | varchar(3) | 支付币种 · 可空 |
| `biz_status` | varchar(32) | 成功-SUCCESS,冲正-REVERSE,撤销-CANCEL,撤销冲正-CANCEL_REVERSE · 可空 |
| `notify_flag` | char | 是否通知 Y-通知 N-不通知 · 可空 |
| `notify_status` | varchar(4) | 通知结果状态 · 可空 |
| `settle_amount` | decimal(15, 4) | 结算金额 · 可空 |
| `settle_currency` | char(3) | 结算币种 · 可空 |
| `recon_extension` | varchar(512) | 对账扩展字段 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_channel_inst_biz`:inst_order_no, fund_channel_code, biz_type (UNIQUE)
- `idx_fund_date_code`:fund_date, fund_channel_code
- `idx_fundflow_clearing_orderno`:clearing_order_no
- `idx_gmt_modified`:gmt_modified
- `idx_paymentSeqNo`:payment_seq_no
- `inx_bill_date_code`:bill_date, fund_channel_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
