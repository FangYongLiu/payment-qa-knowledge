---
id: tbl_ppc_t_corporation_funds_transfer
object_type: Table
name: Corporation Funds Transfer (t_corporation_funds_transfer)
aliases: [t_corporation_funds_transfer, ppc.t_corporation_funds_transfer]
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

# Corporation Funds Transfer (t_corporation_funds_transfer)

## 用途
物理表 `ppc.t_corporation_funds_transfer`,主键 `voucher_no`。Corporation Funds Transfer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_no` | bigint | Voucher No: Voucher No |
| `orig_voucher_no` | bigint | Orig Voucher No · 可空 |
| `request_order_no` | varchar(32) | Request Order No |
| `corporation_id` | varchar(50) | Corporation ID |
| `payee_proxy_number` | varchar(20) | Payee Proxy Number |
| `opt_type` | char | Operate Type: T=Transfer, R=Revert |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `status` | varchar(2) | Status: C=Created Order, S=Success, F=Failed, RP=Revert Processing,RS=Revert Success,RF=Revert Fail |
| `subject` | varchar(100) | Subject |
| `payee_member_id` | varchar(20) | Payee Member ID · 可空 |
| `payer_fee` | decimal(19, 4) | Payer Fee · 可空 |
| `fail_code` | varchar(50) | Fail Code · 可空 |
| `fail_message` | varchar(200) | Fail Message · 可空 |
| `trx_ref_no` | varchar(20) | Trx Ref No · 可空 |
| `batch_no` | varchar(32) | Batch No · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`voucher_no`
- `idx_orig_voucher_no`:orig_voucher_no
- `idx_request_order_no`:request_order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
