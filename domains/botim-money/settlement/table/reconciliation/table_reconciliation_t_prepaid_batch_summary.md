---
id: tbl_reconciliation_t_prepaid_batch_summary
object_type: Table
name: 预付费卡批次对账汇总表 (t_prepaid_batch_summary)
aliases: [t_prepaid_batch_summary, reconciliation.t_prepaid_batch_summary]
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

# 预付费卡批次对账汇总表 (t_prepaid_batch_summary)

## 用途
物理表 `reconciliation.t_prepaid_batch_summary`,主键 `id`。预付费卡批次对账汇总表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前八后九 |
| `batch_id` | varchar(32) | 批次号 |
| `settlement_amount` | decimal(19, 4) | 结算金额 |
| `email_settlement_amount` | decimal(19, 4) | 邮件结算金额 · 可空 |
| `settlement_currency` | char(3) | 结算币种 |
| `ipm_fees` | decimal(19, 4) | IPM费用 · 可空 |
| `markup_fees` | decimal(19, 4) | MARKUP费用 · 可空 |
| `acuiring_fees` | decimal(19, 4) | Acuiring Fees · 可空 |
| `vat_amount` | decimal(19, 4) | 税费金额 · 可空 |
| `net_amount` | decimal(19, 4) | 净额 · 可空 |
| `recon_status` | char | 对账状态 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(512) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_batchId_currency`:batch_id, settlement_currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
