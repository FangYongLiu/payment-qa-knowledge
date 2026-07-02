---
id: tbl_bps_t_employee_source_bulk
object_type: Table
name: Employee original information batch form (t_employee_source_bulk)
aliases: [t_employee_source_bulk, bps.t_employee_source_bulk]
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

# Employee original information batch form (t_employee_source_bulk)

## 用途
物理表 `bps.t_employee_source_bulk`,主键 `id`。Employee original information batch form。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `request_type` | varchar(32) | request type |
| `total_quantity` | int | total quantity |
| `botim_quantity` | int | botim users quantity |
| `non_botim_quantity` | int | non-botim users quantity |
| `submit_quantity` | int | submit quantity |
| `approved_quantity` | int | approved quantity · 可空 |
| `reject_quantity` | int | reject quantity · 可空 |
| `submit_date` | timestamp | submit date · 可空 |
| `approved_date` | timestamp | approved date · 可空 |
| `invoice_id` | varchar(32) | invoice id · 可空 |
| `file_id` | char(32) | File Unique Identifier · 可空 |
| `maker_id` | varchar(64) | maker id · 可空 |
| `approver_id` | varchar(64) | approver id · 可空 |
| `merchant_mid` | varchar(64) | merchant mid · 可空 |
| `parent_merchant_mid` | varchar(64) | parent merchant mid · 可空 |
| `status` | varchar(20) | status |
| `reason` | varchar(255) | reason · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
