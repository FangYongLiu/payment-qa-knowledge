---
id: tbl_eminstalment_t_repay_split
object_type: Table
name: 账单（bill）核销分账表 (t_repay_split)
aliases: [t_repay_split, eminstalment.t_repay_split]
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

# 账单（bill）核销分账表 (t_repay_split)

## 用途
物理表 `eminstalment.t_repay_split`,主键 `id`。账单（bill）核销分账表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 主键 · 可空 |
| `trade_id` | int | 交易记录id，对应t_trade_order表的id |
| `bill_id` | int | 账单id，对应t_bill表的id |
| `repay_principal` | decimal(15, 2) | 本金 |
| `repay_instalment_fee` | decimal(15, 2) | 利息 |
| `repay_penalty` | decimal(15, 2) | 罚息 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `currency` | char(3) | 货币 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
