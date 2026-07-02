---
id: tbl_installmentcard_t_ic_pm_product
object_type: Table
name: Product identity (stable). Installment card product definition (t_ic_pm_product)
aliases: [t_ic_pm_product, installmentcard.t_ic_pm_product]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Product identity (stable). Installment card product definition (t_ic_pm_product)

## 用途
物理表 `installmentcard.t_ic_pm_product`,主键 `id`。Product identity (stable). Installment card product definition。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key for product (stable identity) · 可空 |
| `product_code` | varchar(50) | Unique business product code |
| `name` | varchar(100) | Product display name |
| `currency` | varchar(3) | Product currency (ISO 4217, e.g., AED) |
| `status` | tinyint | Product status: 0=INACTIVE, 1=ACTIVE |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_product_code`:product_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
