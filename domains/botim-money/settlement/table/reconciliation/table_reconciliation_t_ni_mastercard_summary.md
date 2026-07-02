---
id: tbl_reconciliation_t_ni_mastercard_summary
object_type: Table
name: NI MASTERCARD SUMMARY (t_ni_mastercard_summary)
aliases: [t_ni_mastercard_summary, reconciliation.t_ni_mastercard_summary]
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

# NI MASTERCARD SUMMARY (t_ni_mastercard_summary)

## 用途
物理表 `reconciliation.t_ni_mastercard_summary`,主键 `id`。NI MASTERCARD SUMMARY。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Id: 8 digits date + 9 digits sequence |
| `bill_date` | char(8) | Bill Date |
| `fundin_amount` | decimal(19, 4) | FundIn Amount · 可空 |
| `refund_amount` | decimal(19, 4) | Refund Amount · 可空 |
| `net_transaction_amount` | decimal(19, 4) | Net Transaction Amount · 可空 |
| `total_processing_usd_amount` | decimal(19, 4) | Total Processing USD Amount · 可空 |
| `total_processing_aed_amount` | decimal(19, 4) | Total Processing AED Amount · 可空 |
| `total_transaction_amount_aed` | decimal(19, 4) | Total Transaction Amount in AED · 可空 |
| `fx_rate` | decimal(15, 8) | FX Rate · 可空 |
| `ipm_fee_usd` | decimal(19, 4) | IPM Fee In USD · 可空 |
| `ipm_fee_aed` | decimal(19, 4) | IPM Fee In AED · 可空 |
| `dispute_administration_fee_usd` | decimal(19, 4) | Dispute Administration Fee USD · 可空 |
| `dispute_administration_fee_aed` | decimal(19, 4) | Dispute Administration Fee AED · 可空 |
| `total_ipm_fee_aed` | decimal(19, 4) | Total IPM Fee In AED · 可空 |
| `project_fee_usd` | decimal(19, 4) | Project Fee In USD · 可空 |
| `project_fee_aed` | decimal(19, 4) | Project Fee In AED · 可空 |
| `charge_back_usd` | decimal(19, 4) | ChargeBack In USD · 可空 |
| `charge_back_aed` | decimal(19, 4) | ChargeBack In AED · 可空 |
| `total_charge_back_aed` | decimal(19, 4) | Total ChargeBack In AED · 可空 |
| `charge_back_fee_usd` | decimal(19, 4) | ChargeBack Fee In USD · 可空 |
| `charge_back_fee_aed` | decimal(19, 4) | ChargeBack Fee In AED · 可空 |
| `net_amount_should_receive` | decimal(19, 4) | Net Amount Should Receive · 可空 |
| `actual_amount_aed` | decimal(19, 4) | Actual Amount AED · 可空 |
| `actual_usd_cr` | decimal(19, 4) | Actual USD Cr · 可空 |
| `actual_received_usd` | decimal(19, 4) | Actual Received USD · 可空 |
| `actual_received_aed` | decimal(19, 4) | Actual Received AED · 可空 |
| `difference_amount` | decimal(19, 4) | Difference Amount · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_bill_date`:bill_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
