---
id: tbl_reconciliation_t_prepaid_date_summary
object_type: Table
name: 预付费卡按日期对账汇总表 (t_prepaid_date_summary)
aliases: [t_prepaid_date_summary, reconciliation.t_prepaid_date_summary]
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

# 预付费卡按日期对账汇总表 (t_prepaid_date_summary)

## 用途
物理表 `reconciliation.t_prepaid_date_summary`,主键 `id`。预付费卡按日期对账汇总表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前八后九 |
| `bill_date` | varchar(8) | 对账日期 |
| `settlement_currency` | char(3) | 结算币种 |
| `settlement_amount` | decimal(19, 4) | 结算金额 |
| `settled_amount` | decimal(19, 4) | 已结算金额 · 可空 |
| `email_settlement_amount` | decimal(19, 4) | 邮件结算金额 · 可空 |
| `ipm_fees` | decimal(19, 4) | IPM费用 · 可空 |
| `markup_fees` | decimal(19, 4) | MARKUP费用 · 可空 |
| `other_fees` | decimal(19, 4) | 其他费用 · 可空 |
| `vat_amount` | decimal(19, 4) | 税费金额 · 可空 |
| `net_calculation_amount` | decimal(19, 4) | 加总净额 · 可空 |
| `net_read_amount` | decimal(19, 4) | 读取净额 · 可空 |
| `recon_status` | char | 对账状态 |
| `fund_settle_amount` | decimal(19, 4) | 资金结算金额 · 可空 |
| `fund_settle_status` | char | 资金结算结果 · 可空 |
| `income_collect_result` | varchar(512) | 收入归集结果 · 可空 |
| `cost_accrual_result` | varchar(512) | 成本计提结果 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(512) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_billdate_currency`:bill_date, settlement_currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
