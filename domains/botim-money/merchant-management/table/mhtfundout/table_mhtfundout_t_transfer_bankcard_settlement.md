---
id: tbl_mhtfundout_t_transfer_bankcard_settlement
object_type: Table
name: t_transfer_bankcard_settlement (t_transfer_bankcard_settlement)
aliases: [t_transfer_bankcard_settlement, mhtfundout.t_transfer_bankcard_settlement]
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

# t_transfer_bankcard_settlement (t_transfer_bankcard_settlement)

## 用途
物理表 `mhtfundout.t_transfer_bankcard_settlement`,主键 `global_id`。t_transfer_bankcard_settlement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `paid_time` | timestamp(3) | paid_time · 可空 |
| `charge_mid` | varchar(32) | charge mid · 可空 |
| `charge_account_type` | varchar(32) | chargeAccountType · 可空 |
| `charge_fee_currency` | char(3) | charge_fee_currency · 可空 |
| `charge_fee_amount` | decimal(19, 2) | charge_fee_amount · 可空 |
| `settlement_currency` | char(3) | settlement_currency · 可空 |
| `settlement_amount` | decimal(19, 2) | settlementAmount · 可空 |
| `refunded_time` | timestamp(3) | refunded_time · 可空 |
| `refund_charge_fee_curr` | char(3) | refund_charge_fee_curr · 可空 |
| `refund_charge_fee_amt` | decimal(19, 2) | refund_charge_fee_amt · 可空 |
| `refund_settlement_curr` | char(3) | refund_settlement_curr · 可空 |
| `refund_settlement_amt` | decimal(19, 2) | refund_settlement_amt · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id`
- `i_tbs_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
