---
id: tbl_household_t_transfer_receive
object_type: Table
name: Transfer Receive (t_transfer_receive)
aliases: [t_transfer_receive, household.t_transfer_receive]
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

# Transfer Receive (t_transfer_receive)

## 用途
物理表 `household.t_transfer_receive`,主键 `receive_id`。Transfer Receive。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `receive_id` | bigint | Receive ID |
| `transfer_voucher_no` | bigint | Transfer Voucher No |
| `identity_type` | char | Identity Type: M=Mobile Number |
| `identity_value` | varchar(32) | Identity Value |
| `member_id` | varchar(20) | Member ID · 可空 |
| `receive_amount` | decimal(19, 4) | Receive Amount |
| `currency` | char(3) | Currency |
| `status` | varchar(16) | Status: Init,Receiving,WaitKyc,Success,PayFail,Closed |
| `receive_request_no` | bigint | Receive Request No · 可空 |
| `extension` | varchar(255) | Extension: showName · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`receive_id`
- `idx_transfer_voucher_no`:transfer_voucher_no
- `idx_update_time_identity_value`:update_time, identity_value

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
