---
id: tbl_bps_t_employee_adjust_record
object_type: Table
name: 员工风控记录 (t_employee_adjust_record)
aliases: [t_employee_adjust_record, bps.t_employee_adjust_record]
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

# 员工风控记录 (t_employee_adjust_record)

## 用途
物理表 `bps.t_employee_adjust_record`,主键 `id`。员工风控记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `employee_id` | char(32) | 员工主键id |
| `type` | varchar(16) | 风控类型 |
| `status` | char(10) | 状态 Init,Success,Fail |
| `memo` | varchar(64) | 备注 · 可空 |
| `retry_times` | int | 重试次数 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
