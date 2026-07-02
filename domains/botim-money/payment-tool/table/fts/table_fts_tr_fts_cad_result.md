---
id: tbl_fts_tr_fts_cad_result
object_type: Table
name: 上传sftp文件后结果 (tr_fts_cad_result)
aliases: [tr_fts_cad_result, fts.tr_fts_cad_result]
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

# 上传sftp文件后结果 (tr_fts_cad_result)

## 用途
物理表 `fts.tr_fts_cad_result`,主键 `id`。上传sftp文件后结果。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 唯一标识符 · 可空 |
| `batch_no` | varchar(32) | 文件批次号 |
| `data_no` | varchar(32) | 自己生成的唯一数据编号 · 可空 |
| `line_no` | char(6) | file line no文件行号 · 可空 |
| `processed_file_name` | varchar(64) | 待补 · 可空 |
| `cad_file_id` | varchar(16) | 待补 · 可空 |
| `result_file_name` | varchar(64) | 待补 · 可空 |
| `result_type` | char(3) | ACK, NAK · 可空 |
| `record_type` | char(3) | ACK, NAK · 可空 |
| `record_status` | char(8) | “ACCEPTED” or “ACCPWEXP” or “REJECTED” · 可空 |
| `result_code` | varchar(16) | 结果码 · 可空 |
| `result_message` | varchar(200) | 待补 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_update` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_fcd_bn_ln`:batch_no, line_no
- `idx_fcr_data_no`:data_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
