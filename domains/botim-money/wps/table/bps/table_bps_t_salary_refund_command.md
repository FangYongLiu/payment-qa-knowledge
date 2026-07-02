---
id: tbl_bps_t_salary_refund_command
object_type: Table
name: 工资退款指令表 (t_salary_refund_command)
aliases: [t_salary_refund_command, bps.t_salary_refund_command]
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

# 工资退款指令表 (t_salary_refund_command)

## 用途
物理表 `bps.t_salary_refund_command`,主键 `id`。工资退款指令表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `salary_load_request_number` | varchar(64) | 转账请求号 |
| `rri_file_id` | varchar(32) | 退款文件id · 可空 |
| `remark` | varchar(128) | 退款备注 · 可空 |
| `status` | char(10) | 退款状态 |
| `origin_ID` | varchar(64) | 请求id |
| `origin_bulk_ID` | varchar(64) | 请求批次id |
| `maker_id` | varchar(25) | 创建者 · 可空 |
| `approver_id` | varchar(25) | 审批者 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
