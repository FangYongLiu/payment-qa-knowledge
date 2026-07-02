---
id: tbl_rnpl_t_rent_contract
object_type: Table
name: Rental Contract Table (t_rent_contract)
aliases: [t_rent_contract, rnpl.t_rent_contract]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Rental Contract Table (t_rent_contract)

## 用途
物理表 `rnpl.t_rent_contract`,主键 `id`。Rental Contract Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_no` | varchar(64) | contract ID |
| `tenant_user_id` | varchar(32) | tenant user id |
| `broker_user_id` | varchar(32) | broker user id |
| `property_id` | int | property id · 可空 |
| `product_type` | smallint | 1:Rent-To-Rent;2:RNPL Loan · 可空 |
| `rent_start_date` | timestamp | rent start date · 可空 |
| `rent_end_date` | timestamp | rent end date · 可空 |
| `months` | int | total number of months included in the rent contract · 可空 |
| `t_total_rent_amount` | decimal(10, 2) | annual rent shown to Tenant · 可空 |
| `t_security_deposit_amount` | decimal(10, 2) | amount of security deposit to be posted by Tenant · 可空 |
| `t_agent_commission_amount` | decimal(10, 2) | amount of agency fee to be paid by Tenant · 可空 |
| `t_admin_fee_amount` | decimal(10, 2) | amount of management fee to be paid by Tenant · 可空 |
| `t_pay_sd_by_rnpl` | smallint | whether the Tenant Payment Deposit is included in the loan: 0: false, 1: true · 可空 |
| `l_annual_rent_amount` | decimal(10, 2) | the amount of rent shown to Landlord. · 可空 |
| `l_cheque_numbers` | int | the landlord collects the rent in several installments. · 可空 |
| `l_receive_rent_date` | timestamp | the landlord has to collect the rent on that day of the month, or rather, pay the landlord on that day · 可空 |
| `currency` | char(3) | currency · 可空 |
| `status` | tinyint | Status: 0: draft; 1: waiting for officer review; -1: officer review rejected; 2: officer review passed, waiting for down payment; -2: tenant cancel contract; 3: tenant pay deposit successfully, pending broker upload paper contract; -3: broker cancel contract; n4: broker upload paper contract successfully, pending contract review; -5: contract review passed; -6: closed (tenant has paid back the money) |
| `t_receive_ads` | smallint | whether t_receive_ads · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_no`:contract_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
