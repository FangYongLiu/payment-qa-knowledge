---
id: tbl_escrow_t_account_flow
object_type: Table
name: 账户明细流水表 (t_account_flow)
aliases: [t_account_flow, escrow.t_account_flow]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 账户明细流水表 (t_account_flow)

## 用途
物理表 `escrow.t_account_flow`,主键 `account_flow_id`。账户明细流水表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_flow_id` | bigint(19) | 账户明细流水ID |
| `member_Id` | varchar(32) | 会员编号 · 可空 |
| `amount` | decimal(19, 4) | 金额 · 可空 |
| `direction` | varchar(4) | 方向 · 可空 |
| `account_date` | varchar(10) | 账单日期 · 可空 |
| `is_skip_netting` | varchar(4) | 是否跳过轧差 · 可空 |
| `is_netting` | varchar(4) | 是否轧差 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `netting_flow_id` | bigint(19) | 轧差流水ID · 可空 |
| `fund_id` | varchar(64) | 资金流水号 · 可空 |
| `voucher_no` | varchar(64) | 交易凭证号 · 可空 |
| `currency` | varchar(8) | 币种 |
| `payment_order_no` | varchar(64) | 交易订单号 · 可空 |
| `trade_type` | varchar(16) | 流水交易类型 · 可空 |
| `biz_product_code` | varchar(32) | 业务产品码 · 可空 |
| `clearing_code` | varchar(32) | 清算码 · 可空 |
| `merchant_name` | varchar(64) | 商户名称 · 可空 |
| `STATUS` | varchar(4) | 状态 · 可空 |
| `account_batch_id` | bigint(19) | 批次处理号 · 可空 |
| `memo` | varchar(255) | memo · 可空 |
| `card_no` | varchar(32) | 虚拟卡号 · 可空 |
| `fund_channel_code` | varchar(16) | 渠道编号 · 可空 |
| `inst_order_no` | varchar(64) | 机构订单流水号 · 可空 |

## 主键 / 索引
- 主键:`account_flow_id`
- `uk_fund_id`:fund_id (UNIQUE)
- `uk_instOrderNo_tradeType`:inst_order_no, trade_type (UNIQUE)
- `idx_accountBatchId`:account_batch_id
- `idx_accountDate`:account_date
- `idx_paymentOrderNo`:payment_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
