---
id: tbl_eminstalment_t_product
object_type: Table
name: 分期产品列表 (t_product)
aliases: [t_product, eminstalment.t_product]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 分期产品列表 (t_product)

## 用途
物理表 `eminstalment.t_product`,主键 `id`。分期产品列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `version` | int | 版本 |
| `product_code` | varchar(32) | 产品代码 |
| `period` | int | 期数 |
| `period_unit` | varchar(16) | MOUNTH |
| `total_profit_rate` | decimal(6, 4) | 产品要收益率，如某三期的产品，此值为0.24，含义是这款产品借出去3期时间内要收借款金额的24%的利息 · 可空 |
| `min_downpayment_rate` | decimal(6, 4) | 最低首付比例，电商分期才有 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `currency` | char(3) | 货币 |

## 主键 / 索引
- 主键:`id`
- `uk_p`:product_code, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
