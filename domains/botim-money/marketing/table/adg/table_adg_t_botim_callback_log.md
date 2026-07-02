---
id: tbl_adg_t_botim_callback_log
object_type: Table
name: Botim callback notification log table (t_botim_callback_log)
aliases: [t_botim_callback_log, adg.t_botim_callback_log]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# Botim callback notification log table (t_botim_callback_log)

## 用途
物理表 `adg.t_botim_callback_log`,主键 `id`。Botim callback notification log table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `notify_id` | varchar(60) | Botim notification unique ID, used for duplicate prevention |
| `notify_timestamp` | bigint | Botim notification timestamp (milliseconds) · 可空 |
| `order_no` | varchar(60) | Botim order number · 可空 |
| `reference_no` | varchar(60) | External reference number · 可空 |
| `order_status` | varchar(10) | Order status: SUCCESS, FAILED, etc. · 可空 |
| `amount_json` | varchar(50) | Amount information (JSON format) · 可空 |
| `request_body` | varchar(500) | Original request body (JSON format, compressed) · 可空 |
| `processing_status` | varchar(10) | Processing status: PROCESSING, SUCCESS, FAILED · 可空 |
| `error_message` | varchar(255) | Processing error message · 可空 |
| `processing_time_ms` | int | Processing time (milliseconds) · 可空 |
| `response_body` | varchar(255) | Response content · 可空 |
| `created_at` | timestamp | Creation timestamp · 可空 |
| `updated_at` | timestamp | Update timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_notify_id`:notify_id (UNIQUE)
- `idx_created_at`:created_at
- `idx_order_no`:order_no
- `idx_reference_no`:reference_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
