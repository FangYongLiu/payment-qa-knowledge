---
id: tbl_reconciliation_t_manual_recon_summary
object_type: Table
name: t_manual_recon_summary (t_manual_recon_summary)
aliases: [t_manual_recon_summary, reconciliation.t_manual_recon_summary]
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

# t_manual_recon_summary (t_manual_recon_summary)

## 用途
物理表 `reconciliation.t_manual_recon_summary`,主键 `flow_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(16) | 渠道编号 |
| `biz_type` | varchar(4) | 业务类型 |
| `bill_date` | date | 对账日期 |
| `recon_type` | varchar(32) | 对账类型 |
| `fund_amount` | decimal(15, 2) | 交易金额 |
| `fund_count` | int(10) | 交易笔数 · 可空 |
| `fund_fee_amount` | decimal(15, 4) | 手续费 · 可空 |
| `fund_vat_amount` | decimal(15, 4) | 增值税 · 可空 |
| `clear_amount` | decimal(15, 2) | 清算金额 · 可空 |
| `clear_count` | int(10) | 清算笔数 · 可空 |
| `clear_fee_amount` | decimal(15, 4) | 清算手续费 · 可空 |
| `clear_vat_amount` | decimal(15, 4) | 清算增值税 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(8) | 对账状态 · 可空 |
| `message` | varchar(200) | 对账结果描述 · 可空 |
| `operator` | varchar(64) | 操作人 · 可空 |
| `fee_voucher_no` | varchar(32) | 手续费凭证号 · 可空 |
| `fee_status` | varchar(8) | 手续费登账状态 · 可空 |
| `fee_message` | varchar(255) | 手续费登账结果 · 可空 |
| `vat_voucher_no` | varchar(32) | 增值税凭证号 · 可空 |
| `vat_status` | varchar(8) | 增值税登账状态 · 可空 |
| `vat_message` | varchar(255) | 增值税登账结果 · 可空 |
| `oss_path` | varchar(64) | OSS 地址 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(500) | 扩展参数 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `bank_date` | timestamp | 银行日期 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
