---
id: tbl_bps_t_monthly_invoice_retry
object_type: Table
name: monthly invoice retry (t_monthly_invoice_retry)
aliases: [t_monthly_invoice_retry, bps.t_monthly_invoice_retry]
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

# monthly invoice retry (t_monthly_invoice_retry)

## 用途
物理表 `bps.t_monthly_invoice_retry`,主键 `id`。monthly invoice retry。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(26) | ulid |
| `merchant_id` | varchar(20) | merchant id |
| `invoice_date` | timestamp | invoice date · 可空 |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
