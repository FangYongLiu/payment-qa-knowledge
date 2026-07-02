---
id: tbl_amlreport_tb_transfer
object_type: Table
name: 转账订单 (tb_transfer)
aliases: [tb_transfer, amlreport.tb_transfer]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# 转账订单 (tb_transfer)

## 用途
物理表 `amlreport.tb_transfer`,主键 `id`。转账订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `payer_id` | varchar(32) | 付款方ID · 可空 |
| `payee_id` | varchar(32) | 收款方ID · 可空 |
| `transfer_amt` | decimal(15, 4) | 转账金额 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `status` | varchar(20) | 状态 · 可空 |
| `transfer_time` | timestamp | 转账发起时间 · 可空 |
| `expire_time` | timestamp | 过期退款时间 · 可空 |
| `transaction_id` | varchar(64) | 交易ID · 可空 |
| `biz_product_code` | varchar(20) | 业务产品码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_transfer_payee_id`:payee_id
- `idx_transfer_payer_id`:payer_id
- `idx_transfer_transfer_time`:transfer_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
