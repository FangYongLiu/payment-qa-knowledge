---
id: tbl_statement_t_statement_template
object_type: Table
name: 对账单模板 (t_statement_template)
aliases: [t_statement_template, statement.t_statement_template]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: statement schema DDL
tags: [settlement, statement]
sensitivity: normal
related_services: []
---

# 对账单模板 (t_statement_template)

## 用途
物理表 `statement.t_statement_template`,主键 `id`。对账单模板。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `statement_type` | varchar(50) | 对账单类型 FUND 资金账单；PURCHASE_TRADE 收单交易账单；REFUND_TRADE 退款交易账单 |
| `period_type` | varchar(50) | 期限类型 DAILY 日账单；MONTHLY 月账单 |
| `created_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `idx_statement_period`:statement_type, period_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
