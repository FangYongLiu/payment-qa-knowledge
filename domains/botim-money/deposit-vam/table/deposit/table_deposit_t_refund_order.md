---
id: tbl_deposit_t_refund_order
object_type: Table
name: Deposit Refund Order (t_refund_order)
aliases: [t_refund_order, deposit.t_refund_order]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# Deposit Refund Order (t_refund_order)

## 用途
物理表 `deposit.t_refund_order`,主键 `refund_voucher_no`。Deposit Refund Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `refund_voucher_no` | bigint | Refund Voucher No: 18 digits, '13' + 10 timestamp digits + 4 sequence digits + 2 random digits |
| `trade_voucher_no` | varchar(32) | Trade Voucher No |
| `client_id` | varchar(32) | Client id |
| `orig_pay_voucher_no` | varchar(32) | Original Pay Voucher No · 可空 |
| `refund_amount` | decimal(19, 4) | Refund Amount |
| `currency` | char(3) | Refund Currency |
| `refund_status` | varchar(16) | Refund status: P: Processing;S: Successful;F failure; |
| `refund_pay_voucher_no` | bigint | Refund pay voucher number · 可空 |
| `control_extension` | varchar(255) | Control Extension · 可空 |
| `unity_result_code` | varchar(50) | Unity result code · 可空 |
| `remark` | varchar(128) | Remark · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `finish_time` | timestamp | Finish Time · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`refund_voucher_no`
- `idx_refund_pay_voucher_no`:refund_pay_voucher_no
- `idx_trade_voucher_no`:trade_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
