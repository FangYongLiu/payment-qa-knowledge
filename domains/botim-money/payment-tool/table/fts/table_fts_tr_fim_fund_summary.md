---
id: tbl_fts_tr_fim_fund_summary
object_type: Table
name: fim fund summary (tr_fim_fund_summary)
aliases: [tr_fim_fund_summary, fts.tr_fim_fund_summary]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fts schema DDL
tags: [payment-tool, fts]
sensitivity: normal
related_services: []
---

# fim fund summary (tr_fim_fund_summary)

## 用途
物理表 `fts.tr_fim_fund_summary`,主键 `id`。fim fund summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `summary_no` | varchar(32) | summary data no |
| `summary_source` | varchar(8) | summary source |
| `summary_date` | date | summary date |
| `total_amount` | decimal(19, 2) | total amount in pre day |
| `status` | char | I,S,F |
| `summary_state` | varchar(8) | INIT,SUBMIT,SUCCESS,FAIL |
| `gmt_create` | timestamp | create time |
| `gmt_update` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `udx_tffs_no`:summary_no (UNIQUE)
- `idx_tffs_ds`:summary_date, summary_source
- `idx_tffs_gct`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
