---
id: tbl_ccexchange_t_trade_param
object_type: Table
name: 交易参数 (t_trade_param)
aliases: [t_trade_param, ccexchange.t_trade_param]
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

# 交易参数 (t_trade_param)

## 用途
物理表 `ccexchange.t_trade_param`,主键 `id`。交易参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `base_currency_code` | varchar(32) | 本位币币种 |
| `base_amount` | decimal(23, 8) | 本位币金额 |
| `quote_amount` | decimal(23, 8) | 报价金额 |
| `quote_currency_code` | varchar(32) | 报价币种 |
| `symbol` | varchar(32) | symbol |
| `direction` | varchar(16) | 买卖方向 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
