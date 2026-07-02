---
id: tbl_rnpl_t_tenant_pay_rent_plan
object_type: Table
name: pay rent plan (t_tenant_pay_rent_plan)
aliases: [t_tenant_pay_rent_plan, rnpl.t_tenant_pay_rent_plan]
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

# pay rent plan (t_tenant_pay_rent_plan)

## 用途
物理表 `rnpl.t_tenant_pay_rent_plan`,主键 `id`。pay rent plan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `tenant_user_id` | varchar(32) | user_id of tenant |
| `contract_id` | int | contract id |
| `cheque_numbers` | int | cheque numbers |
| `cheque_no` | smallint | cheque no |
| `due_time` | timestamp | due time · 可空 |
| `total_rent_amount` | decimal(10, 2) | is prepaid_rent_amount+loan_amount · 可空 |
| `tenant_prepaid_amount` | decimal(10, 2) |  is (deposit_amount + total_rent_amount)/cheue_numbers (from t_rent_contract) |
| `loan_amount` | decimal(10, 2) | is deposit_amount+total_rent_amount-tenant_prepaid_amount |
| `handling_fee` | decimal(10, 2) | handling fee |
| `dp_amount` | decimal(10, 2) |  is prepaid_rent_amount  + handling_fee |
| `dp_expired_time` | timestamp | dp_expired_time · 可空 |
| `finish_pay_time` | timestamp | finish_pay_time · 可空 |
| `status` | smallint | 待补 |
| `loan_product_id` | int | loan product id |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
