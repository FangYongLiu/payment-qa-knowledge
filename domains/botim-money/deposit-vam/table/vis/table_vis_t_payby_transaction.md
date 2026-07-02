---
id: tbl_vis_t_payby_transaction
object_type: Table
name: Unique Index for Bank Order No (t_payby_transaction)
aliases: [t_payby_transaction, vis.t_payby_transaction]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# Unique Index for Bank Order No (t_payby_transaction)

## 用途
物理表 `vis.t_payby_transaction`,主键 `transaction_id`。Unique Index for Bank Order No。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | bigint(17) | Transaction Id |
| `member_id` | varchar(32) | Member id |
| `dpm_account_type` | varchar(10) | BASIC-basic, WPS_SALARY - wps |
| `beneficiary_account` | varchar(32) | Benificiary Account |
| `beneficiary_name` | varchar(32) | Beneficiary name · 可空 |
| `direction` | char | I-FundIn,O-FundOut · 可空 |
| `bank_order_no` | varchar(32) | File Order No, Unique and idempotent condition |
| `transaction_status` | char | Transaction status · 可空 |
| `sender_bic` | varchar(11) | Sender bank id code · 可空 |
| `transaction_type_code` | char(3) | MWO · 可空 |
| `amount` | decimal(19, 4) | Transaction Amount |
| `currency` | char(3) | AED |
| `fee` | decimal(19, 4) | Inner Fee |
| `sender_customer` | varchar(32) | Customer Info · 可空 |
| `reference_no` | varchar(32) | Reference No · 可空 |
| `deposit_voucher_no` | varchar(32) | Deposit Voucher No · 可空 |
| `payment_order_no` | varchar(32) | Payment Order No · 可空 |
| `inner_trans_code` | varchar(16) | Inner Trans Code · 可空 |
| `inner_trans_message` | varchar(128) | Inner Trans message · 可空 |
| `on_account_status` | char | On Account Status, Y-Yes, N-No, W-Writeoff · 可空 |
| `on_account_voucher_no` | varchar(32) | On Account Voucher No · 可空 |
| `audit_record_id` | bigint(19) | Audit Record Id · 可空 |
| `writeoff_able_amount` | decimal(19, 4) | Writeoff Able Amount · 可空 |
| `gmt_trans` | timestamp | Trans time · 可空 |
| `extension` | varchar(1024) | Extension Feild · 可空 |
| `gmt_create` | timestamp | Create time |
| `gmt_modified` | timestamp | Modify time · 可空 |
| `gmt_retry` | timestamp | Retry time · 可空 |

## 主键 / 索引
- 主键:`transaction_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
