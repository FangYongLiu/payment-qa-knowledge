---
id: tbl_visii_t_vam_order
object_type: Table
name: Unique Index for Bank and Bank Order No (t_vam_order)
aliases: [t_vam_order, visii.t_vam_order]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: visii schema DDL
tags: [deposit-vam, visii]
sensitivity: normal
related_services: []
---

# Unique Index for Bank and Bank Order No (t_vam_order)

## 用途
物理表 `visii.t_vam_order`,主键 `order_id`。Unique Index for Bank and Bank Order No。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_id` | bigint | Order Id |
| `bank_code` | varchar(5) | Bank Code, ZAND/PAYBY |
| `member_id` | varchar(20) | Member id · 可空 |
| `va_type` | char(2) | va type, VA-virtual account |
| `account_type` | varchar(10) | BASIC-basic, WPS_SALARY - wps · 可空 |
| `iban` | varchar(20) | Benificiary Iban |
| `direction` | char | I-FundIn,O-FundOut · 可空 |
| `bank_order_no` | varchar(32) | Bank Order No, Unique and idempotent condition |
| `status` | varchar(2) | status,WV/VF/V/R/F/S |
| `source` | varchar(4) | Source: VAM/LEAN · 可空 |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | AED |
| `fee` | decimal(19, 4) | Fee · 可空 |
| `reference_no` | varchar(32) | Reference No · 可空 |
| `deposit_voucher_no` | bigint(22) | Deposit Voucher No · 可空 |
| `payment_order_no` | bigint(22) | Payment Order No · 可空 |
| `result_code` | varchar(20) | Result code · 可空 |
| `result_message` | varchar(128) | Result Message · 可空 |
| `gmt_trans` | timestamp(3) | Trans time · 可空 |
| `extension` | varchar(512) | Extension Feild · 可空 |
| `gmt_create` | timestamp(3) | Create time |
| `gmt_modified` | timestamp(3) | Modify time · 可空 |
| `gmt_finished` | timestamp(3) | Finish time · 可空 |

## 主键 / 索引
- 主键:`order_id`
- `idx_va_order_dep_voucher_no`:deposit_voucher_no
- `idx_va_order_modify_time_mid`:member_id, gmt_modified

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
