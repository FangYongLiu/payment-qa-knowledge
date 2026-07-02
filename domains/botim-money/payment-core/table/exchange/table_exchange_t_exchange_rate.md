---
id: tbl_exchange_t_exchange_rate
object_type: Table
name: t_exchange_rate (t_exchange_rate)
aliases: [t_exchange_rate, exchange.t_exchange_rate]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: exchange schema DDL
tags: [payment-core, exchange]
sensitivity: normal
related_services: []
---

# t_exchange_rate (t_exchange_rate)

## 用途
物理表 `exchange.t_exchange_rate`,主键 `exchange_rate_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `exchange_rate_id` | bigint(17) | 汇率id |
| `source_currency` | varchar(3) | 源币种 |
| `target_currency` | varchar(3) | 目标币种 |
| `supplier` | varchar(32) | 供应商 |
| `exchange_date` | date | 汇率日期 |
| `exchange_rate` | decimal(19, 8) | Exchange Rate · 可空 |
| `status` | char | 状态 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`exchange_rate_id`
- `uk_exchange_rate_day`:source_currency, target_currency, supplier, exchange_date (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
