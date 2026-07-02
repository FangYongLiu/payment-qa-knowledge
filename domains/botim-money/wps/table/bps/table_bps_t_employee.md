---
id: tbl_bps_t_employee
object_type: Table
name: 员工表 (t_employee)
aliases: [t_employee, bps.t_employee]
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

# 员工表 (t_employee)

## 用途
物理表 `bps.t_employee`,主键 `id`。员工表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `tenant_code` | varchar(32) | 商户号 |
| `employee_number` | varchar(32) | 员工编码 |
| `full_name` | varchar(250) | full name |
| `passport_number` | varchar(100) | 护照 · 可空 |
| `EID` | varchar(100) | EID · 可空 |
| `EID_expiry` | varchar(100) | EID过期日期 · 可空 |
| `employee_profile_id` | char(32) | 员工档案信息id · 可空 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
