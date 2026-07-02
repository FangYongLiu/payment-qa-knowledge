---
id: tbl_installmentcard_t_ic_stm_statement_generation_run
object_type: Table
name: Operational audit for statement generation batch jobs (t_ic_stm_statement_generation_run)
aliases: [t_ic_stm_statement_generation_run, installmentcard.t_ic_stm_statement_generation_run]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Operational audit for statement generation batch jobs (t_ic_stm_statement_generation_run)

## 用途
物理表 `installmentcard.t_ic_stm_statement_generation_run`,主键 `id`。Operational audit for statement generation batch jobs。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `run_date` | date | Business date for statement generation run |
| `status` | tinyint | Run status: 0=STARTED, 1=COMPLETED, 2=FAILED |
| `total_accounts_processed` | int | Number of accounts processed |
| `total_statements_generated` | int | Number of statements generated successfully |
| `started_at` | datetime | When the run started · 可空 |
| `completed_at` | datetime | When the run completed (success or failure) · 可空 |
| `error_message` | varchar(1000) | Error message if run failed · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |
| `pdf_generated_count` | int | PDFs successfully generated in this run |
| `pdf_failed_count` | int | PDFs that failed in this run |

## 主键 / 索引
- 主键:`id`
- `idx_run_date`:run_date
- `idx_started_at`:started_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
