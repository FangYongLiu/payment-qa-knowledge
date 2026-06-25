---
id: tbl_aml_t_chargeback_pool
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_chargeback_pool
subdomain: aml
module: null
sensitivity: normal
name: chargeback pool(t_chargeback_pool)
aliases:
- t_chargeback_pool
related_services:
- svc_aml
related_scenarios: []
---
# chargeback pool(t_chargeback_pool)

## 用途
chargeback pool。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `case_no` | varchar(64) | NOT NULL | caseNo |
| `merchant_id` | varchar(20) |  | merchantId |
| `merchant_name` | varchar(128) |  | merchantName |
| `member_id` | varchar(20) |  | memberID |
| `mcc` | varchar(20) |  | mcc |
| `transaction_id` | varchar(64) |  | transactionId |
| `payment_order_no` | varchar(64) |  | paymentOrderNo |
| `inst_order_no` | varchar(64) |  | instOrderNo |
| `acquirer` | varchar(32) | NOT NULL | acquirer |
| `arn` | varchar(32) | NOT NULL | arn |
| `case_type` | varchar(32) | NOT NULL | caseType |
| `case_status` | varchar(32) | NOT NULL | caseStatues |
| `channel_status` | varchar(32) | NOT NULL | channelStatus |
| `transaction_amount` | decimal(15,4) | NOT NULL | transactionAmount |
| `transaction_currency` | char(3) | NOT NULL | transactionCurrency |
| `reason_code` | varchar(32) |  | reasonCode |
| `reason_description` | varchar(200) |  | reasonDescription |
| `evidence_due_date` | timestamp |  | evidenceDueDate |
| `chargeback_date` | timestamp |  | chargebackDate |
| `transaction_date` | timestamp |  | transactionDate |
| `auth_code` | varchar(32) |  | authCode |
| `chargeback_amount` | decimal(15,4) |  | chargeback_amount |
| `chargeback_currency` | char(3) |  | chargeback_currency |
| `chargeback_reason` | varchar(200) |  | chargeback_reason |
| `card_no` | varchar(30) |  | card_no |
| `card_first_six` | char(6) |  | card_first_six |
| `card_last_four` | char(4) |  | card_last_four |
| `extension` | varchar(2000) |  | extension |
| `created_by` | varchar(32) | NOT NULL | created_by |
| `updated_by` | varchar(32) | NOT NULL | updated_by |
| `valid` | tinyint(1) | NOT NULL / 默认 1 | valid |
| `label` | varchar(128) |  | label |
| `biz_product_code` | varchar(10) |  | biz product code |
| `partner_name` | varchar(20) |  | partner name |
| `next_send_time` | timestamp(3) |  | mail next send time |
| `create_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | createTime |
| `update_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | updateTime |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_case_no` (case_no)
  - `idx_merchant_id` (merchant_id)
  - `idx_payment_order_no` (payment_order_no)
  - `idx_transaction_id` (transaction_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
