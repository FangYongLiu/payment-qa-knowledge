---
id: tbl_bps_t_employee_profile
object_type: Table
name: 员工档案信息表 (t_employee_profile)
aliases: [t_employee_profile, bps.t_employee_profile]
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

# 员工档案信息表 (t_employee_profile)

## 用途
物理表 `bps.t_employee_profile`,主键 `id`。员工档案信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `title` | varchar(20) | 称谓 · 可空 |
| `first_name` | varchar(125) | first name |
| `middle_name` | varchar(64) | 中间名字 · 可空 |
| `last_name` | varchar(125) | last name |
| `mother_name` | varchar(64) | 母亲姓名 · 可空 |
| `DOB` | char(10) | 出生日期 |
| `gender` | char | 性别 M,F |
| `country_code` | char(2) | 国家简码 |
| `nationality` | varchar(64) | country code |
| `qrCode` | varchar(256) | 二维码 · 可空 |
| `tenant_code` | varchar(32) | 商户号 |
| `name_on_card` | varchar(250) | name on card |
| `occupation` | varchar(100) | Employee occupation · 可空 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
