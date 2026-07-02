---
id: tbl_creditinvoice_t_letter_qr_code
object_type: Table
name: QR code record table (t_letter_qr_code)
aliases: [t_letter_qr_code, creditinvoice.t_letter_qr_code]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# QR code record table (t_letter_qr_code)

## 用途
物理表 `creditinvoice.t_letter_qr_code`,主键 `id`。QR code record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | 待补 · 可空 |
| `qr_id` | varchar(64) | qr_id for 16 chars |
| `eid` | varchar(64) | UES ticket |
| `eid_hash` | varchar(64) | SHA-256(eid_plain + EidHashUtil.SALT) |
| `biz_type` | varchar(32) | LIABILITY_LETTER / NO_LIABILITY_LETTER |
| `publisher_name` | varchar(128) | e.g. Quantix |
| `letter_date` | date | Issue date yyyy-MM-dd |
| `valid_from` | timestamp | qr id validate time since |
| `valid_until` | timestamp | qr id validate time until |
| `source` | varchar(16) | STANDALONE / LETTER |
| `related_request_no` | varchar(32) | Phase 1 letter association · 可空 |
| `extra_info` | varchar(512) | Extra JSON: invalidatedReason / supersededByQrId / operator / reason · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_qr_id`:qr_id (UNIQUE)
- `idx_eid_hash`:eid_hash
- `idx_related_request`:related_request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
