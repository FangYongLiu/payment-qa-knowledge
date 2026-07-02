---
id: tbl_rnpl_t_public_holidays
object_type: Table
name: Table to store public holidays (t_public_holidays)
aliases: [t_public_holidays, rnpl.t_public_holidays]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Table to store public holidays (t_public_holidays)

## 用途
物理表 `rnpl.t_public_holidays`,主键 `id`。Table to store public holidays。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `holiday_date` | date | Date of the public holiday |
| `holiday_name` | varchar(255) | Name of the public holiday |
| `country` | varchar(100) | Country where the holiday is observed · 可空 |
| `created_at` | timestamp | Record creation time · 可空 |
| `updated_at` | timestamp | Record last update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `unique_holiday_date`:holiday_date, country (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
