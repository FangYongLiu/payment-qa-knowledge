---
id: tbl_household_t_hh_prepaid_card_beneficiary_order
object_type: Table
name: prepaid card beneficiary order (t_hh_prepaid_card_beneficiary_order)
aliases: [t_hh_prepaid_card_beneficiary_order, household.t_hh_prepaid_card_beneficiary_order]
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

# prepaid card beneficiary order (t_hh_prepaid_card_beneficiary_order)

## 用途
物理表 `household.t_hh_prepaid_card_beneficiary_order`,主键 `id`。prepaid card beneficiary order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `order_id` | varchar(32) | order id |
| `owner_id` | varchar(32) | owner id |
| `member_id` | varchar(32) | member id |
| `card_type` | varchar(32) | card type |
| `amount` | decimal(19, 4) | amount |
| `currency` | char(3) | currency |
| `expire_time` | timestamp | expire time |
| `status` | varchar(32) | status |
| `created_at` | timestamp | created time |
| `updated_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
