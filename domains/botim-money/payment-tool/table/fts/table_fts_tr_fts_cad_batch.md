---
id: tbl_fts_tr_fts_cad_batch
object_type: Table
name: 批次上传sftp的文件数据 (tr_fts_cad_batch)
aliases: [tr_fts_cad_batch, fts.tr_fts_cad_batch]
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

# 批次上传sftp的文件数据 (tr_fts_cad_batch)

## 用途
物理表 `fts.tr_fts_cad_batch`,主键 `id`。批次上传sftp的文件数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 唯一标识符 · 可空 |
| `batch_no` | varchar(32) | 文件批次号 |
| `batch_type` | varchar(9) | EMPTY, NOT_EMPTY |
| `entity_id` | char(3) | default 413 · 可空 |
| `submit_date` | date | yyyy-MM-dd |
| `sequence_no` | char(6) | 待补 |
| `file_name` | varchar(64) | 待补 · 可空 |
| `total_count` | int(5) | 待补 |
| `status` | char |  I S F  I:initial,S:suceess,F:FAILED · 可空 |
| `state` | varchar(12) | INIT,FILE_DONE,FILE_SUBMIT,SEMI_SUCCESS,SUCCESS,FAILD · 可空 |
| `extension` | varchar(1024) | 待补 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_update` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `udx_fcb_batch_no`:batch_no (UNIQUE)
- `idx_fcb_submit_date`:submit_date

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
