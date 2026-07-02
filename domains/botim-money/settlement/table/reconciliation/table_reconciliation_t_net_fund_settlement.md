---
id: tbl_reconciliation_t_net_fund_settlement
object_type: Table
name: 净额资金结算记录 (t_net_fund_settlement)
aliases: [t_net_fund_settlement, reconciliation.t_net_fund_settlement]
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

# 净额资金结算记录 (t_net_fund_settlement)

## 用途
物理表 `reconciliation.t_net_fund_settlement`,主键 `flow_id`。净额资金结算记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(64) | 渠道编号 · 可空 |
| `fund_source` | varchar(64) | Fund Source · 可空 |
| `amount` | decimal(16, 4) | 金额 · 可空 |
| `carried_amount` | decimal(15, 4) | 已结转金额 · 可空 |
| `uncarried_amount` | decimal(15, 4) | 待结转金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `start_date` | date | 起始日期 · 可空 |
| `end_date` | date | 截止日期 · 可空 |
| `bank_date` | date | 银行入账日期 · 可空 |
| `bank_reference` | varchar(64) | 银行流水号 · 可空 |
| `status` | varchar(16) | 结算状态 · 可空 |
| `message` | varchar(64) | 结算信息 · 可空 |
| `settle_order_no` | varchar(64) | 结算单号 · 可空 |
| `cr_account_no` | varchar(32) | 贷方账号 · 可空 |
| `dr_account_no` | varchar(32) | 借方账号 · 可空 |
| `source_order_type` | varchar(16) | Source Order Type · 可空 |
| `source_order_no` | varchar(32) | Source Order No · 可空 |
| `operator` | varchar(32) | 操作人 · 可空 |
| `memo` | varchar(255) | 结算备注 · 可空 |
| `bank_memo` | varchar(128) | 银行备注 · 可空 |
| `extension` | varchar(512) | 扩展信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_bank_reference`:bank_reference (UNIQUE)
- `idx_chennel_code_date`:fund_channel_code, start_date, end_date
- `idx_ordertype_orderno`:source_order_type, source_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
