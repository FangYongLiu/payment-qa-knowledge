---
id: tbl_escrow_t_report_file
object_type: Table
name: PTPR Report File (t_report_file)
aliases: [t_report_file, escrow.t_report_file]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# PTPR Report File (t_report_file)

## 用途
物理表 `escrow.t_report_file`,主键 `report_file_id`。PTPR Report File。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `report_file_id` | bigint(32) | Report File id |
| `bank_code` | varchar(4) | bank code : FAB |
| `file_date` | char(8) | file date: yyyyMMdd · 可空 |
| `dr_records` | int(10) | dr records · 可空 |
| `dr_amount` | decimal(19, 4) | dr amount · 可空 |
| `cr_records` | int(10) | cr records |
| `cr_amount` | decimal(19, 4) | cr amount |
| `status` | char | File status: I-Initial, R-Retry, S-Submitted, F-Failed · 可空 |
| `gmt_start` | char(8) | start time: yyyyMMdd · 可空 |
| `gmt_end` | char(8) | end time: yyyyMMdd · 可空 |
| `gmt_create` | timestamp(6) | create time |
| `gmt_modified` | timestamp(6) | modify time · 可空 |
| `extension` | varchar(512) | Extension · 可空 |

## 主键 / 索引
- 主键:`report_file_id`
- `uk_re_file_bank_date`:bank_code, file_date (UNIQUE)
- `indx_re_file_gmt_create`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
