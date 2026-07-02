---
id: tbl_bps_t_withdraw_central_bank_account_record
object_type: Table
name: withdraw central bank account record (t_withdraw_central_bank_account_record)
aliases: [t_withdraw_central_bank_account_record, bps.t_withdraw_central_bank_account_record]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# withdraw central bank account record (t_withdraw_central_bank_account_record)

## 用途
物理表 `bps.t_withdraw_central_bank_account_record`,主键 `id`。withdraw central bank account record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `trade_request_no` | varchar(64) | trade request no |
| `payroll_bulk_id` | varchar(32) | payroll bulk id · 可空 |
| `corporate_id` | varchar(32) | corporate id · 可空 |
| `corporate_registration_id` | varchar(32) | corporate mol id |
| `corporate_name` | varchar(200) | corporate name · 可空 |
| `corporate_account` | varchar(32) | corporate account · 可空 |
| `central_bank_account` | varchar(64) | central bank account · 可空 |
| `status` | varchar(10) | status |
| `load_amount` | decimal(11, 2) | load amount |
| `message` | varchar(255) | response message · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
