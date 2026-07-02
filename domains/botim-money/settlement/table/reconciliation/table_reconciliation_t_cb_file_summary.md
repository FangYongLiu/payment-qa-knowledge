---
id: tbl_reconciliation_t_cb_file_summary
object_type: Table
name: 央行文件汇总表 (t_cb_file_summary)
aliases: [t_cb_file_summary, reconciliation.t_cb_file_summary]
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

# 央行文件汇总表 (t_cb_file_summary)

## 用途
物理表 `reconciliation.t_cb_file_summary`,主键 `id`。央行文件汇总表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前8后9 · 可空 |
| `trade_date` | char(8) | 交易日期 |
| `start_amount` | decimal(19, 4) | 日初金额 · 可空 |
| `end_amount` | decimal(19, 4) | 日终金额 · 可空 |
| `debit_count` | int | Debit总笔数 · 可空 |
| `debit_total_amount` | decimal(19, 4) | Debit交易总额 · 可空 |
| `credit_count` | int | Credit总笔数 · 可空 |
| `credit_total_amount` | decimal(19, 4) | Credit交易总额 · 可空 |
| `net_amount` | decimal(19, 4) | 交易净额 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_trade_date`:trade_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
