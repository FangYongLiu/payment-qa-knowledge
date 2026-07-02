---
id: tbl_bps_t_corp_invoice_fee_item_code
object_type: Table
name: corporate invoice fee item code (t_corp_invoice_fee_item_code)
aliases: [t_corp_invoice_fee_item_code, bps.t_corp_invoice_fee_item_code]
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

# corporate invoice fee item code (t_corp_invoice_fee_item_code)

## 用途
物理表 `bps.t_corp_invoice_fee_item_code`,主键 `id`。corporate invoice fee item code。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `fee_code_id` | varchar(32) | fee code id |
| `item_code` | varchar(10) | item code |
| `description` | varchar(100) | description |
| `charge_amount` | decimal(19, 4) | charge amount |
| `status` | varchar(10) | status |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
