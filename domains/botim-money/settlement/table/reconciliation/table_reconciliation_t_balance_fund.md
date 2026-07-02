---
id: tbl_reconciliation_t_balance_fund
object_type: Table
name: 余额对账入账流水 (t_balance_fund)
aliases: [t_balance_fund, reconciliation.t_balance_fund]
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

# 余额对账入账流水 (t_balance_fund)

## 用途
物理表 `reconciliation.t_balance_fund`,主键 `flow_id`。余额对账入账流水。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 流水ID 主键 |
| `fund_channel_code` | varchar(16) | 渠道编号 · 可空 |
| `bank_code` | varchar(8) | 银行编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型IOB · 可空 |
| `flow_type` | varchar(8) | 流水类型 登账、入金等 · 可空 |
| `bank_date` | timestamp | 银行交易时间 · 可空 |
| `bill_date` | date | 对账日期 · 可空 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `fee_amount` | decimal(15, 2) | 手续费 · 可空 |
| `vat_amount` | decimal(15, 2) | 增值税 · 可空 |
| `inst_order_no` | varchar(32) | 机构订单号 · 可空 |
| `bank_reference` | varchar(32) | 银行流水号 · 可空 |
| `status` | varchar(8) | 对账状态 · 可空 |
| `extension` | varchar(1024) | 扩展信息 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `message` | varchar(255) | 入账流水信息 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
