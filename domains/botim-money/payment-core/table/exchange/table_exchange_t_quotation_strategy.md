---
id: tbl_exchange_t_quotation_strategy
object_type: Table
name: t_quotation_strategy (t_quotation_strategy)
aliases: [t_quotation_strategy, exchange.t_quotation_strategy]
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

# t_quotation_strategy (t_quotation_strategy)

## 用途
物理表 `exchange.t_quotation_strategy`,主键 `quotation_strategy_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `quotation_strategy_id` | bigint(17) | 报价策略id |
| `source_currency` | varchar(7) | 源币种 · 可空 |
| `target_currency` | varchar(7) | 目标币种 · 可空 |
| `channel_code` | varchar(16) | 渠道 · 可空 |
| `fixed_percent` | decimal(19, 4) | Fixed Percent · 可空 |
| `fixed_amount` | decimal(19, 4) | Fixed Amount · 可空 |
| `status` | char | 状态:Y-生效 N-失效 · 可空 |
| `gmt_effect` | timestamp | 生效时间 · 可空 |
| `gmt_expired` | timestamp | 过期时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`quotation_strategy_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
