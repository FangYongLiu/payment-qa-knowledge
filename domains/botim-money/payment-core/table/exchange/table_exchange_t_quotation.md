---
id: tbl_exchange_t_quotation
object_type: Table
name: t_quotation (t_quotation)
aliases: [t_quotation, exchange.t_quotation]
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

# t_quotation (t_quotation)

## 用途
物理表 `exchange.t_quotation`,主键 `quotation_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `quotation_id` | bigint(18) | 报价id |
| `quotation_strategy_id` | bigint(17) | 报价策略id · 可空 |
| `source_amount` | decimal(19, 4) | Source Amount |
| `source_currency` | varchar(3) | 源币种 |
| `target_amount` | decimal(19, 4) | Target Amount |
| `target_currency` | varchar(3) | 目标币种 |
| `client_id` | varchar(32) | 客户端id · 可空 |
| `member_id` | varchar(32) | 会员id |
| `gmt_expired` | timestamp | 过期时间 · 可空 |
| `status` | varchar(8) | 状态 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `extension` | varchar(256) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`quotation_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
