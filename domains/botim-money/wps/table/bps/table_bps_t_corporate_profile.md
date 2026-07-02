---
id: tbl_bps_t_corporate_profile
object_type: Table
name: corporate profile info (t_corporate_profile)
aliases: [t_corporate_profile, bps.t_corporate_profile]
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

# corporate profile info (t_corporate_profile)

## 用途
物理表 `bps.t_corporate_profile`,主键 `id`。corporate profile info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `trade_license_number` | varchar(64) | trade license number · 可空 |
| `trade_license_expiry` | varchar(16) | trade license expiry · 可空 |
| `free_zone` | varchar(64) | free zone · 可空 |
| `tax_no` | varchar(64) | tax num · 可空 |
| `contact_person` | varchar(100) | contact person · 可空 |
| `contact_person_address` | varchar(255) | contact person address · 可空 |
| `contact_person_eid` | varchar(32) | contact person eid · 可空 |
| `contact_person_mobile_no` | varchar(16) | contact person mobile no · 可空 |
| `contact_person_city` | varchar(64) | contact person city · 可空 |
| `contact_person_country` | varchar(32) | contact person country · 可空 |
| `contact_person_email_address` | varchar(100) | contact person email address · 可空 |
| `products_assigned` | varchar(100) | products assigned · 可空 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |
| `sponsor_person_eid` | varchar(255) | Sponsor Person EID · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
