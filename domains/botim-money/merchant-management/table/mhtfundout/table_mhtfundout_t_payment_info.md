---
id: tbl_mhtfundout_t_payment_info
object_type: Table
name: t_payment_info (t_payment_info)
aliases: [t_payment_info, mhtfundout.t_payment_info]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# t_payment_info (t_payment_info)

## 用途
物理表 `mhtfundout.t_payment_info`,主键 `global_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `payer_fee_currency` | varchar(50) | 付款币种 · 可空 |
| `payer_fee_amount` | decimal(19, 4) | 付款金额 · 可空 |
| `arrival_time` | timestamp(3) | 预期到达时间 · 可空 |
| `charge_mid` | varchar(32) | charge mid · 可空 |
| `charge_account_type` | varchar(32) | chargeAccountType · 可空 |
| `settlement_currency` | char(3) | settlement_currency · 可空 |
| `settlement_amount` | decimal(19, 2) | settlementAmount · 可空 |
| `refunded_time` | timestamp(3) | refunded_time · 可空 |
| `refund_charge_fee_curr` | char(3) | refund_charge_fee_curr · 可空 |
| `refund_charge_fee_amt` | decimal(19, 2) | refund_charge_fee_amt · 可空 |
| `refund_settlement_curr` | char(3) | refund_settlement_curr · 可空 |
| `refund_settlement_amt` | decimal(19, 2) | refund_settlement_amt · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
