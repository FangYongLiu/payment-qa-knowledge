---
id: tbl_ccexchange_t_currency_pair_exchange
object_type: Table
name: 币对转换配置 (t_currency_pair_exchange)
aliases: [t_currency_pair_exchange, ccexchange.t_currency_pair_exchange]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccexchange schema DDL
tags: [crypto, ccexchange]
sensitivity: normal
related_services: []
---

# 币对转换配置 (t_currency_pair_exchange)

## 用途
物理表 `ccexchange.t_currency_pair_exchange`,主键 `product_pair`。币对转换配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_pair` | varchar(32) | 产品币对 |
| `channel` | varchar(32) | 交易id |
| `execution_pair` | varchar(32) | 执行币对 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`product_pair`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
