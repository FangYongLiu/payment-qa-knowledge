---
id: tbl_coupon_t_supplier
object_type: Table
name: 供应商 (t_supplier)
aliases: [t_supplier, coupon.t_supplier]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 供应商 (t_supplier)

## 用途
物理表 `coupon.t_supplier`,主键 `supplier_id`。供应商。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `supplier_id` | bigint | 主键 |
| `supplier_logo` | varchar(128) | 供应商logo · 可空 |
| `supplier_name` | varchar(64) | 供应商名称 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`supplier_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
