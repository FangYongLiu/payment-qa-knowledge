---
id: tbl_afis_t_payment_receipt
object_type: Table
name: payment receipt (t_payment_receipt)
aliases: [t_payment_receipt, afis.t_payment_receipt]
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

# payment receipt (t_payment_receipt)

## 用途
物理表 `afis.t_payment_receipt`,主键 `id`。payment receipt。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `payment_session_id` | char(32) | payment session id |
| `aifi_order_id` | char(32) | aifi order id |
| `aifi_order_amount` | decimal(10, 2) | order amount |
| `customer_uid` | char(32) | aifi customer uid |
| `customer_phone` | char(20) | aifi customer phone number |
| `send_status` | char(10) | sms sending status: ToSend|Sending|Sent|Failed |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
