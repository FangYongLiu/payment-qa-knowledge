---
id: tbl_rtp_t_payer_order
object_type: Table
name: Payer Order (t_payer_order)
aliases: [t_payer_order, rtp.t_payer_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rtp schema DDL
tags: [online-business, rtp]
sensitivity: normal
related_services: []
---

# Payer Order (t_payer_order)

## 用途
物理表 `rtp.t_payer_order`,主键 `payer_order_no`。Payer Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payer_order_no` | bigint | Payer Order No: voucher no |
| `payee_order_no` | bigint | Payee Order No · 可空 |
| `aani_rtp_id` | bigint | Aani Rtp Id · 可空 |
| `member_id` | varchar(20) | Member Id |
| `rtp_method` | varchar(10) | Rtp Method: BOTIM/AANI |
| `amount` | decimal(19, 4) | Amount |
| `fee` | decimal(19, 4) | Fee |
| `currency` | char(3) | Currency |
| `reason` | varchar(140) | Reason · 可空 |
| `status` | varchar(10) | Status: I=Init, E=Expired, R=Rejected, C=Cancelled, PS=PaySuccess, SC=SettleConfirmed, CP=CancelProcess, CS=CancelSuccess |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `io_type` | varchar(10) | Io Type: I2I,O2I · 可空 |
| `pay_trade_no` | bigint | Pay Trade No · 可空 |
| `settle_voucher_no` | bigint | Settle Voucher No · 可空 |
| `cancel_voucher_no` | bigint | Cancel Voucher No · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `expire_time` | timestamp | Expire Time |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |
| `finish_time` | timestamp | Finish Time · 可空 |

## 主键 / 索引
- 主键:`payer_order_no`
- `uidk_payer_aani_rtp_id`:aani_rtp_id, rtp_method (UNIQUE)
- `idx_expire_time_status`:expire_time, status
- `idx_pay_trade_no`:pay_trade_no
- `idx_payee_order_no`:payee_order_no
- `idx_update_time_mid`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
