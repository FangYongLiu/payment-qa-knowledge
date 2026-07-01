---
id: tbl_remittance_t_beneficiary_account_info
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_beneficiary_account_info
subdomain: remittance
module: null
sensitivity: normal
name: 受益人账户信息表(t_beneficiary_account_info)
aliases:
- t_beneficiary_account_info
related_services:
- svc_remittance
related_scenarios: []
---
# 受益人账户信息表(t_beneficiary_account_info)

## 用途
受益人账户信息表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `beneficiary_info_id` | bigint | NOT NULL | 受益人id |
| `transaction_mode` | varchar(16) | NOT NULL | 收款模式;CASH_PICK_UP,BANK_TRANSFER,MOBILE_WALLET |
| `holder_name` | varchar(255) |  | 持卡人姓名 |
| `country_code` | char(3) |  | 国家ISO code |
| `account_no` | varchar(80) |  | 账户号 |
| `iban` | varchar(32) |  | Iban |
| `wallet_code` | varchar(32) |  | 账户code |
| `wallet_name` | varchar(255) |  | 账户名称;如支付宝，微信 |
| `account_type` | varchar(32) |  | Saving, Current |
| `bank_code` | varchar(16) |  | 银行CODE |
| `bank_name` | varchar(255) |  | 银行名称 |
| `branch_name` | varchar(255) |  | 分支行名称 |
| `branch_code` | varchar(32) |  | 分支行名称 |
| `intermediary_bank` | varchar(32) |  | 中间行BIC的CODE |
| `mobile_no` | varchar(32) |  | 手机号;银行预留手机号 |
| `mobile_country` | char(3) |  | 手机号所属国家 |
| `routing_code` | varchar(32) |  | 银行routingCode;如IFSC |
| `swift_code` | varchar(32) |  | 银行swiftCode |
| `bank_identify_id` | varchar(32) |  | 账户信息编号;如sort code，routing number |
| `alias` | varchar(255) |  | 别名 |
| `currency` | char(3) |  | 币种 |
| `enable_flag` | char | NOT NULL | 启用标识: Y=启用，N=停用 |
| `memo` | varchar(255) |  | 备注 |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `counting` | int(12) |  | 计数 |
| `last_commit_time` | timestamp |  | 上次汇款时间 |
| `err_flag` | char |  | SF |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_beneficiary_info_id` (beneficiary_info_id)
  - `idx_create_time` (create_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
