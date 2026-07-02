---
id: tbl_reconciliation_t_auto_settlement
object_type: Table
name: 自动结算表 (t_auto_settlement)
aliases: [t_auto_settlement, reconciliation.t_auto_settlement]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 自动结算表 (t_auto_settlement)

## 用途
物理表 `reconciliation.t_auto_settlement`,主键 `id`。自动结算表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前八后九 |
| `auto_settlement_type` | varchar(16) | 结算类型 |
| `bill_date` | char(8) | 对账日期 |
| `onaccount_id` | bigint | 挂账id · 可空 |
| `settlement_id` | bigint | 商户结算id · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `target_currency` | char(3) | 目标币种 |
| `status` | char(3) | 状态 |
| `result_message` | varchar(255) | 结果信息 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_type_date_currency`:auto_settlement_type, bill_date, currency (UNIQUE)
- `idx_settlementId`:settlement_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
