---
id: tbl_fts_tr_qpay_fts_batch
object_type: Table
name: fund transfer CTC (tr_qpay_fts_batch)
aliases: [tr_qpay_fts_batch, fts.tr_qpay_fts_batch]
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

# fund transfer CTC (tr_qpay_fts_batch)

## 用途
物理表 `fts.tr_qpay_fts_batch`,主键 `id`。fund transfer CTC。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 唯一标识符 · 可空 |
| `source` | varchar(30) | 系统来源 |
| `source_reference_no` | varchar(32) | 来源编号 |
| `batch_no` | varchar(16) | 批次编号 |
| `transaction_type` | char | B,S |
| `institution_identifier` | varchar(13) | 机构标识 · 可空 |
| `submit_date` | date | 提交时间 · 可空 |
| `total_count` | int(10) | 总数量 |
| `total_amount` | decimal(19, 2) | 总金额 |
| `status` | char | I:INITIAL,S:SUCCESS,F:FAILED |
| `state` | varchar(12) | INIT,PROCESS,SUCCESS,FAILED,NOTIFIED,这条数据上传状态流转 |
| `file_name` | varchar(128) | 文件名称 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_update` | timestamp | 修改时间 |
| `submit_time` | timestamp | submit time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_batch_no`:batch_no
- `idx_batch_source`:source, source_reference_no
- `idx_tqfb_st`:submit_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
