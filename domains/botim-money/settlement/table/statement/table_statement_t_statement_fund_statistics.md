---
id: tbl_statement_t_statement_fund_statistics
object_type: Table
name: 资金对账单统计信息 (t_statement_fund_statistics)
aliases: [t_statement_fund_statistics, statement.t_statement_fund_statistics]
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

# 资金对账单统计信息 (t_statement_fund_statistics)

## 用途
物理表 `statement.t_statement_fund_statistics`,主键 `id`。资金对账单统计信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `file_id` | bigint | 文件id |
| `total_income` | decimal(19, 4) | 总收入 |
| `income_nums` | int | 总收入笔数 |
| `total_payout` | decimal(19, 4) | 总支出 |
| `payout_nums` | int | 总支出笔数 |
| `opening_amount` | decimal(19, 4) | 期初余额 |
| `ending_amount` | decimal(19, 4) | 期末余额 |
| `currency_code` | varchar(20) | 币种 |
| `created_time` | timestamp | 创建时间 |
| `merchant_mid` | varchar(32) | 商户ID · 可空 |
| `period_type` | varchar(32) | 期限类型 · 可空 |
| `begin_date` | timestamp | 开始时间 · 可空 |
| `end_date` | timestamp | 结束时间 · 可空 |
| `statement_type` | varchar(32) | 对账单类型 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uidx_file_id`:file_id (UNIQUE)
- `inx_begin_date`:begin_date

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
