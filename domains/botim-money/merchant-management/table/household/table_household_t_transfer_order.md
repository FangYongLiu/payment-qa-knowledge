---
id: tbl_household_t_transfer_order
object_type: Table
name: Transfer Order (t_transfer_order)
aliases: [t_transfer_order, household.t_transfer_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# Transfer Order (t_transfer_order)

## 用途
物理表 `household.t_transfer_order`,主键 `transfer_voucher_no`。Transfer Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transfer_voucher_no` | bigint | Transfer Voucher No |
| `request_no` | varchar(64) | Request No: Out request no |
| `transfer_type` | char(2) | Transfer Type: AR=Auth Transfer, CM=Cashier Merge |
| `payer_id` | varchar(20) | Payer ID |
| `merchant_id` | varchar(20) | Merchant ID |
| `transfer_amount` | decimal(19, 4) | Transfer Amount |
| `currency` | char(3) | Currency |
| `receive_count` | int | Receive Count |
| `status` | varchar(16) | Status: WaitPay,PaySuccess,Refunding,Refunded,Closed,ReceiveCompleted |
| `received_count` | int | Received Count |
| `received_amount` | decimal(19, 4) | Received Amount |
| `refund_amount` | decimal(19, 4) | Refund Amount · 可空 |
| `pay_request_no` | bigint | Pay Request No · 可空 |
| `refund_request_no` | bigint | Refund Request No · 可空 |
| `extension` | varchar(255) | Extension: Extension: proxyProtocolNo, description · 可空 |
| `expire_time` | timestamp | Expire Time |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`transfer_voucher_no`
- `idx_expire_time`:expire_time
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
