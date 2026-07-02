---
id: tbl_ppc_t_fx_pol_order
object_type: Table
name: Foreign Exchange Profit or Loss (t_fx_pol_order)
aliases: [t_fx_pol_order, ppc.t_fx_pol_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Foreign Exchange Profit or Loss (t_fx_pol_order)

## 用途
物理表 `ppc.t_fx_pol_order`,主键 `order_id`。Foreign Exchange Profit or Loss。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_id` | bigint | Order ID: 8 + 9 digits |
| `relate_voucher_no` | bigint | Relate Voucher Number |
| `relate_voucher_type` | varchar(10) | Relate Voucher Type: FX=Foreign Exchange, T=Transaction, RT=Revert Transaction |
| `source_amount` | decimal(19, 4) | Source Amount |
| `source_currency` | char(3) | Source Currency |
| `source_rate_version` | bigint | Source Rate Version · 可空 |
| `target_amount` | decimal(19, 4) | Target Amount |
| `target_currency` | char(3) | Target Currency |
| `target_rate_version` | bigint | Target Rate Version · 可空 |
| `pol_status` | varchar(10) | Status: P=Processing, CS=Calculation Success, BS=Balance Success, AS=Accounting Success |
| `cal_type` | varchar(10) | Calculation Type: S=Sell, B=Buy, BS=Buy and sell, RB=Revert Buy · 可空 |
| `buying_hold_amount` | decimal(19, 4) | Buying Hold Amount · 可空 |
| `buying_pol_amount` | decimal(19, 4) | Buying Profit or Loss Amount · 可空 |
| `selling_hold_amount` | decimal(19, 4) | Selling Hold Amount · 可空 |
| `selling_pol_amount` | decimal(19, 4) | Selling Profit or Loss Amount · 可空 |
| `buying_remain_version` | bigint | Buying Remain Version · 可空 |
| `selling_remain_version` | bigint | Selling Remain Version · 可空 |
| `payment_voucher_no` | bigint | Payment Voucher Number · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |

## 主键 / 索引
- 主键:`order_id`
- `uk_relate_voucher_no_type`:relate_voucher_no, relate_voucher_type (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
