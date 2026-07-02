---
id: tbl_ppc_t_3ds_session_record
object_type: Table
name: 3DS authentication session record table (t_3ds_session_record)
aliases: [t_3ds_session_record, ppc.t_3ds_session_record]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# 3DS authentication session record table (t_3ds_session_record)

## 用途
物理表 `ppc.t_3ds_session_record`,主键 `session_record_id`。3DS authentication session record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `session_record_id` | bigint | Session record id;First 8,last 9(Primary Key) |
| `session_id` | varchar(64) | session id (from yse) |
| `txn_ref_no` | varchar(32) | Transaction reference number (from YSE) |
| `proxy_number` | varchar(20) | Virtual card proxy number |
| `merchant_name` | varchar(100) | Merchant name · 可空 |
| `merchant_id` | varchar(50) | Merchant identifier · 可空 |
| `mcc_code` | char(4) | Merchant category code · 可空 |
| `transaction_amount` | decimal(19, 4) | Transaction Amount: From Mastercard |
| `transaction_currency` | char(3) | Transaction Currency |
| `txn_time` | timestamp | Transaction time |
| `acs_client_ip` | varchar(20) | Acs Client IP address · 可空 |
| `expiration_time` | timestamp | Session expiration time |
| `auth_status` | varchar(20) | Authentication status (CREATED/NOTIFIED/DENIED/EXPIRED/CARD_BLOCKED/SUCCESS/FAIL) |
| `fail_code` | varchar(50) | Fail code · 可空 |
| `cis_ticket` | varchar(32) | Cis ticket · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`session_record_id`
- `uk_session_id`:session_id (UNIQUE)
- `idx_expiration_auth`:expiration_time, auth_status
- `idx_proxy_number`:proxy_number
- `idx_txn_ref_no`:txn_ref_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
