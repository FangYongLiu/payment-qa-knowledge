---
id: tbl_bps_t_payroll_paf
object_type: Table
name: payroll paf info (t_payroll_paf)
aliases: [t_payroll_paf, bps.t_payroll_paf]
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

# payroll paf info (t_payroll_paf)

## 用途
物理表 `bps.t_payroll_paf`,主键 `id`。payroll paf info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `request_ref_number` | varchar(64) | request ref number |
| `corporate_mol_id` | varchar(64) | corporate mol id |
| `process_type` | varchar(10) | process type |
| `employee_count` | varchar(16) | employee count |
| `total_amount` | varchar(16) | total amount |
| `pay_period` | varchar(16) | pay period |
| `status` | varchar(10) | status |
| `retry_flag` | varchar(10) | retry flag · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
