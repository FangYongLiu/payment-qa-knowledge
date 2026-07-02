---
id: tbl_reconciliation_t_ni_visa_summary
object_type: Table
name: NI VISA SUMMARY (t_ni_visa_summary)
aliases: [t_ni_visa_summary, reconciliation.t_ni_visa_summary]
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

# NI VISA SUMMARY (t_ni_visa_summary)

## 用途
物理表 `reconciliation.t_ni_visa_summary`,主键 `id`。NI VISA SUMMARY。业务语义细节**待补**(表结构来自 DDL)。

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
| `fx_rate` | decimal(15, 8) | FX Rate · 可空 |
| `total_transaction_amount_aed` | decimal(19, 4) | Total Transaction Amount AED · 可空 |
| `actual_fee` | decimal(19, 4) | Actual Fee · 可空 |
| `other_fee` | decimal(19, 4) | Other Fee · 可空 |
| `charge_back` | decimal(19, 4) | Charge Back · 可空 |
| `charge_back_check` | char | Charge Back Check: Y: yes N:No · 可空 |
| `net_amount_should_receive` | decimal(19, 4) | Net Amount Should Receive · 可空 |
| `domestic_settlement_amount` | decimal(19, 4) | Domestic Settlement Amount · 可空 |
| `domestic_settlement_status` | char | Domestic Settlement Status: S:Settled U:Unsettled · 可空 |
| `international_settlement_amount` | decimal(19, 4) | International Settlement Amount · 可空 |
| `international_settlement_status` | char | International Settlement Status: S:Settled U:Unsettled · 可空 |
| `total_settlement_amount` | decimal(19, 4) | Total Settlement Amount · 可空 |
| `difference_amount` | decimal(19, 4) | Difference_Amount · 可空 |
| `fee_rate` | decimal(15, 8) | Fee Rate · 可空 |
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
