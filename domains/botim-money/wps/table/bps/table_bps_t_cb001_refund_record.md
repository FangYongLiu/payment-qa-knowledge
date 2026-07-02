---
id: tbl_bps_t_cb001_refund_record
object_type: Table
name: cb001 refund record (t_cb001_refund_record)
aliases: [t_cb001_refund_record, bps.t_cb001_refund_record]
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

# cb001 refund record (t_cb001_refund_record)

## 用途
物理表 `bps.t_cb001_refund_record`,主键 `id`。cb001 refund record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `trade_request_no` | varchar(64) | trade request no |
| `payroll_bulk_id` | varchar(32) | payroll bulk id |
| `corporate_registration_id` | varchar(32) | corporate mol id |
| `corporate_name` | varchar(200) | corporate name |
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
