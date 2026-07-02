---
id: tbl_bps_t_employee_deactivation_history
object_type: Table
name: employee deactivation history (t_employee_deactivation_history)
aliases: [t_employee_deactivation_history, bps.t_employee_deactivation_history]
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

# employee deactivation history (t_employee_deactivation_history)

## 用途
物理表 `bps.t_employee_deactivation_history`,主键 `id`。employee deactivation history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `employee_id` | varchar(32) | employee id |
| `corporate_id` | varchar(32) | corporate id |
| `deactive_time` | timestamp | deactive time |
| `operater` | varchar(20) | operater |
| `createAt` | timestamp | createAt |
| `updateAt` | timestamp | updateAt |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
