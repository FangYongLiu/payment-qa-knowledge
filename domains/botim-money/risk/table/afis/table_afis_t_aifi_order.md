---
id: tbl_afis_t_aifi_order
object_type: Table
name: AiFi pushed order (t_aifi_order)
aliases: [t_aifi_order, afis.t_aifi_order]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: afis schema DDL
tags: [risk, afis]
sensitivity: normal
related_services: []
---

# AiFi pushed order (t_aifi_order)

## 用途
物理表 `afis.t_aifi_order`,主键 `id`。AiFi pushed order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `oid` | int | AiFi Order ID |
| `session_id` | varchar(50) | the unique ID sent to AiFi system to identify one session group |
| `status` | char(20) | IN-AiFi-System order status |
| `store_id` | int | AiFi Store ID, started at 1 |
| `store_external_id` | varchar(50) | External AiFi Store ID |
| `customer_uid` | varchar(50) | AiFi customer user id |
| `customer_external_id` | varchar(50) | External AiFi customer user id |
| `customer_role` | char(10) | AiFi customer user role |
| `amount` | decimal(10, 2) | total amount |
| `total_price` | char(15) | total price |
| `total_tax` | char(15) | total tax |
| `subtotal_price` | char(15) | subtotal price |
| `payment_provider` | char(10) | payment provider |
| `payment_status` | char(15) | payment status in AiFi system |
| `pi_type` | char(15) | payment instrument type: card |
| `pi_card_last4` | char(4) | card last four digits |
| `pi_card_exp_month` | int | card exp month |
| `pi_card_exp_year` | int | card exp year |
| `pi_card_brand` | char(10) | card brand |
| `time_of_origin` | char(30) | origin ISO time |
| `time_of_issue` | char(30) | issue ISO time |
| `psp_handle_status` | char(10) | PSP handling status |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_aifi_order_oid_index`:oid (UNIQUE)
- `uk_aifi_order_session_id_index`:session_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
