---
id: tbl_bps_t_employee_address
object_type: Table
name: 员工地址信息表 (t_employee_address)
aliases: [t_employee_address, bps.t_employee_address]
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

# 员工地址信息表 (t_employee_address)

## 用途
物理表 `bps.t_employee_address`,主键 `id`。员工地址信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `country` | varchar(32) | 国家 · 可空 |
| `state` | varchar(32) | 地区 · 可空 |
| `city` | varchar(32) | 城市 · 可空 |
| `address1` | varchar(100) | 地址1 · 可空 |
| `address2` | varchar(100) | 地址2 · 可空 |
| `address3` | varchar(100) | 地址3 · 可空 |
| `address4` | varchar(100) | 地址4 · 可空 |
| `postcode` | char(6) | 邮编 · 可空 |
| `phone_no` | varchar(14) | 固话 · 可空 |
| `tenant_code` | varchar(32) | 商户号 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
