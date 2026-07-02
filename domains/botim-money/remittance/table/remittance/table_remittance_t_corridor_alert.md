---
id: tbl_remittance_t_corridor_alert
object_type: Table
name: REM-617: Corridor availability alert subscriptions (t_corridor_alert)
aliases: [t_corridor_alert, remittance.t_corridor_alert]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# REM-617: Corridor availability alert subscriptions (t_corridor_alert)

## 用途
物理表 `remittance.t_corridor_alert`,主键 `id`。REM-617: Corridor availability alert subscriptions。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | Member ID |
| `partner_id` | varchar(20) | Partner ID (required for PNS notification) |
| `platform_uid` | varchar(128) | Botim platform identity (for PNS delivery) |
| `receiver_country` | varchar(8) | Receiver country code, e.g. EG |
| `receiver_currency` | varchar(8) | Receiver currency code, e.g. EGP |
| `transaction_mode` | varchar(32) | BANK_TRANSFER / MOBILE_WALLET / CASH_PICK_UP |
| `routing_payload` | varchar(1024) | Full CorridorBom JSON for route retry |
| `status` | tinyint | 0=PENDING, 1=NOTIFIED, 2=CANCELLED |
| `created_at` | timestamp | Creation timestamp |
| `notified_at` | timestamp | When notification was sent · 可空 |
| `updated_at` | timestamp | Update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_member_corridor`:member_id, receiver_country, receiver_currency, transaction_mode (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
