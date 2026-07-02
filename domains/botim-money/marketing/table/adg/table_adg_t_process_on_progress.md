---
id: tbl_adg_t_process_on_progress
object_type: Table
name: Tracks the progress of various application processes (t_process_on_progress)
aliases: [t_process_on_progress, adg.t_process_on_progress]
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

# Tracks the progress of various application processes (t_process_on_progress)

## 用途
物理表 `adg.t_process_on_progress`,主键 `id`。Tracks the progress of various application processes。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Unique identifier, primary key · 可空 |
| `app_code` | varchar(31) | Application code |
| `user_id` | varchar(63) | User identifier |
| `loan_id` | varchar(63) | Loan product identifier |
| `process_name` | varchar(127) | Name of the ongoing process · 可空 |
| `process_ref_id` | varchar(127) | unique id for the request · 可空 |
| `state` | varchar(63) | Current state of the process · 可空 |
| `autofill_json` | varchar(5120) | JSON data for autofill or process state (stored encrypted) · 可空 |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Record last update timestamp |
| `encryption_version` | tinyint | Encryption version: -2=pending migration, -1=corrupted, 2=AES-GCM |

## 主键 / 索引
- 主键:`id`
- `idx_app_code_user_id_loan_id`:app_code, user_id, loan_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
