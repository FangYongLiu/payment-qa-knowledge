---
id: tbl_ppcenter_t_dcc_markup_record
object_type: Table
name: Final effective DCC markup records per merchant product order (t_dcc_markup_record)
aliases: [t_dcc_markup_record, ppcenter.t_dcc_markup_record]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppcenter schema DDL
tags: [activation, ppcenter]
sensitivity: normal
related_services: []
---

# Final effective DCC markup records per merchant product order (t_dcc_markup_record)

## 用途
物理表 `ppcenter.t_dcc_markup_record`,主键 `id`。Final effective DCC markup records per merchant product order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `rate` | decimal(10, 6) | Markup rate |
| `product_order_id` | bigint | FK to t_merchant_product_order.id |
| `status` | tinyint(1) | 1=Active, 0=Inactive (deactivated) |
| `gmt_effective` | timestamp | Markup record effective date · 可空 |
| `gmt_invalid` | timestamp | Markup record invalid date · 可空 |
| `gmt_create` | timestamp | Markup record create date |
| `gmt_modify` | timestamp | Markup record create date |
| `memo` | varchar(128) | Memo or remark · 可空 |
| `member_id` | varchar(20) | Member ID or Merchant ID · 可空 |
| `biz_product_code` | varchar(64) | Biz product code or mapping product code · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_product_order_id`:product_order_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
