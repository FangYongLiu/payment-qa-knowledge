---
id: tbl_credit_t_cs_clearance_certificate
object_type: Table
name: loan clearance certificate records (t_cs_clearance_certificate)
aliases: [t_cs_clearance_certificate, credit.t_cs_clearance_certificate]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# loan clearance certificate records (t_cs_clearance_certificate)

## 用途
物理表 `credit.t_cs_clearance_certificate`,主键 `id`。loan clearance certificate records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `user_id` | varchar(20) | member id |
| `order_no` | varchar(64) | order no in chain; normal equals root |
| `root_order_no` | varchar(64) | root order no of refinance chain |
| `certificate_type` | varchar(16) | normal | refinance |
| `document_issue_date` | timestamp | certificate issue datetime · 可空 |
| `file_tag` | varchar(128) | ufs object path for generated pdf |
| `created_time` | timestamp | created time · 可空 |
| `updated_time` | timestamp | updated time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)
- `idx_root_order_no`:root_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
