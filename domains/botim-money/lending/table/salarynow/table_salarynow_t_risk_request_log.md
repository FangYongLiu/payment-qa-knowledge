---
id: tbl_salarynow_t_risk_request_log
object_type: Table
name: t_risk_request_log (t_risk_request_log)
aliases: [t_risk_request_log, salarynow.t_risk_request_log]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# t_risk_request_log (t_risk_request_log)

## 用途
物理表 `salarynow.t_risk_request_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | Member identifier |
| `application_id` | bigint | Application identifier |
| `request_payload` | varchar(1024) | Request body sent to risk system |
| `response_payload` | varchar(1024) | Response body from risk system · 可空 |
| `http_status` | int | HTTP status from risk system · 可空 |
| `request_sent_at` | timestamp | When request was sent |
| `response_received_at` | timestamp | When response arrived · 可空 |
| `created_at` | timestamp | Row creation time |
| `updated_at` | timestamp | Last update time |

## 主键 / 索引
- 主键:`id`
- `uq_no_duplicate`:member_id, application_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
