---
id: tbl_fts_tr_fts_fim_batch
object_type: Table
name: tr_fts_fim_batch (tr_fts_fim_batch)
aliases: [tr_fts_fim_batch, fts.tr_fts_fim_batch]
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

# tr_fts_fim_batch (tr_fts_fim_batch)

## 用途
物理表 `fts.tr_fts_fim_batch`,主键 `id`。tr_fts_fim_batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique ID · 可空 |
| `filename` | varchar(100) | filename like E035413C1031032402270092291.FTR |
| `source` | char(3) |  from 2nd to 4th in the file name. remitter bank code.like 035 |
| `file_date` | char(6) | yyMMdd |
| `total_count` | int(6) | file records · 可空 |
| `total_amount` | decimal(19, 2) | 待补 · 可空 |
| `source_filename` | varchar(32) | EC103035711078240227100504.FTS · 可空 |
| `source_batch_no` | varchar(32) | source 103 file CTC batch no  NFR/24/006494131 · 可空 |
| `extension` | varchar(255) | backup · 可空 |
| `status` | char | I,S,F |
| `state` | varchar(12) | INIT,SUBMIT,SUCCESS,FAILED |
| `gmt_create` | timestamp | create time |
| `gmt_update` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `udx_tffb_sbns`:source_batch_no, source (UNIQUE)
- `idx_tffb_fdsf`:source_filename, file_date
- `idx_tffb_gct`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
