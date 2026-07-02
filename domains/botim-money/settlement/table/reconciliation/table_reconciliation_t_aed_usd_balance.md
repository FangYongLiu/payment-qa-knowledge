---
id: tbl_reconciliation_t_aed_usd_balance
object_type: Table
name: AED/USD BALANCE (t_aed_usd_balance)
aliases: [t_aed_usd_balance, reconciliation.t_aed_usd_balance]
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

# AED/USD BALANCE (t_aed_usd_balance)

## 用途
物理表 `reconciliation.t_aed_usd_balance`,主键 `id`。AED/USD BALANCE。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id: 8 digits date + 9 digits sequence |
| `source_type` | char | Source Type: I: Internal E:External |
| `fund_channel_code` | varchar(32) | Fund Channel Code |
| `currency` | char(3) | Currency |
| `bill_date` | char(8) | Bill Date |
| `opening_balance` | decimal(19, 4) | Opening Balance · 可空 |
| `deposit_amount` | decimal(19, 4) | FundIn Amount · 可空 |
| `withdrawal_amount` | decimal(19, 4) | Refund Amount · 可空 |
| `fee_amount` | decimal(19, 4) | Fee Amount · 可空 |
| `revenue_commission` | decimal(19, 4) | Revenue Commission · 可空 |
| `closing_balance` | decimal(19, 4) | Close Balance · 可空 |
| `difference_amount` | decimal(19, 4) | Difference Amount · 可空 |
| `adjust_flag` | char | Adjust Flag: Y:Yes N:No · 可空 |
| `status` | char | Status: S: Success F:Failed · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_unique_check`:fund_channel_code, source_type, bill_date, currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
