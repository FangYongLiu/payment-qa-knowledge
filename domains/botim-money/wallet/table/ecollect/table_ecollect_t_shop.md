---
id: tbl_ecollect_t_shop
object_type: Table
name: Shop core table (t_shop)
aliases: [t_shop, ecollect.t_shop]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Shop core table (t_shop)

## 用途
物理表 `ecollect.t_shop`,主键 `id`。Shop core table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | Shop ID |
| `owner_id` | varchar(8) | Shop owner Botim UID |
| `level` | varchar(8) | Shop level: L1, L2, L3 |
| `admin_name` | varchar(64) | Admin display name (L2 mandatory) · 可空 |
| `email` | varchar(128) | Admin email (L2 mandatory) · 可空 |
| `admin_phone` | varchar(20) | Admin phone with country code (L2 mandatory) · 可空 |
| `receiving_account_type` | varchar(30) | Receiving account type |
| `payment_merchant_no` | varchar(32) | Payment merchant no (L3 only) · 可空 |
| `product_limit` | int | Product limit |
| `oa_id` | varchar(8) | Botim Public Account ID · 可空 |
| `oa_client_id` | varchar(64) | Botim OA OAuth client id (L2) · 可空 |
| `oa_client_secret` | varchar(256) | Botim OA OAuth client secret (L2; internal only, never expose) · 可空 |
| `oa_pns_account` | varchar(32) | Botim PNS account for OA push · 可空 |
| `oa_activated_at` | timestamp | Open shop time · 可空 |
| `oa_deactivated_at` | timestamp | Close shop time · 可空 |
| `oa_register_id` | varchar(32) | OA registration id for status polling · 可空 |
| `oa_status` | varchar(16) | INIT / SUCCESS / REJECTED; NULL never applied · 可空 |
| `oa_rejected_reason` | varchar(255) | Reason text when approval rejected · 可空 |
| `oa_rejected_at` | datetime | Approval rejected timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_oa_id`:oa_id (UNIQUE)
- `uk_owner_id`:owner_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
