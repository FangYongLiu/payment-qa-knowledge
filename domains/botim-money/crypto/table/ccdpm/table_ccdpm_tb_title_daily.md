---
id: tbl_ccdpm_tb_title_daily
object_type: Table
name: 科目每日信息 (tb_title_daily)
aliases: [tb_title_daily, ccdpm.tb_title_daily]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 科目每日信息 (tb_title_daily)

## 用途
物理表 `ccdpm.tb_title_daily`,主键 `id`。科目每日信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID |
| `account_date` | char(8) | 会计日 |
| `title_code` | varchar(16) | 科目代码 |
| `currency` | varchar(10) | 币种 |
| `balance_direction` | char | 余额方向 |
| `debit_amount` | decimal(19, 8) | 借方发生额 · 可空 |
| `credit_amount` | decimal(19, 8) | 贷方发生额 · 可空 |
| `debit_count` | decimal(15) | 借方发生笔数 · 可空 |
| `credit_count` | decimal(15) | 贷方发生笔数 · 可空 |
| `debit_balance` | decimal(19, 8) | 借方余额 · 可空 |
| `credit_balance` | decimal(19, 8) | 贷方余额 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_account_date_title_code`:account_date, title_code (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
