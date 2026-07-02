---
id: tbl_instalment_t_ci_sku
object_type: Table
name: 商品SKU (t_ci_sku)
aliases: [t_ci_sku, instalment.t_ci_sku]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 商品SKU (t_ci_sku)

## 用途
物理表 `instalment.t_ci_sku`,主键 `id`。商品SKU。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 主健 · 可空 |
| `imei` | varchar(50) | 手机IMEI · 可空 |
| `brand` | varchar(50) | 品牌 · 可空 |
| `model` | varchar(50) | 型号 · 可空 |
| `is_confirm` | char(3) | 是否确认 · 可空 |
| `attrs` | varchar(255) | 手机属性 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_imei`:imei

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
