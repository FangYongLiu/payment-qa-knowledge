---
id: tbl_reconciliation_t_file_parse_script_log
object_type: Table
name: 文件解析日志 (t_file_parse_script_log)
aliases: [t_file_parse_script_log, reconciliation.t_file_parse_script_log]
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

# 文件解析日志 (t_file_parse_script_log)

## 用途
物理表 `reconciliation.t_file_parse_script_log`,主键 `log_id`。文件解析日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint | 待补 |
| `parse_batch_no` | varchar(32) | 对账单解析批次编号 · 可空 |
| `file_seq_no` | varchar(32) | 清算文件编号 · 可空 |
| `script_id` | int | 解析脚本编号 · 可空 |
| `script_name` | varchar(32) | 待补 · 可空 |
| `file_type` | varchar(8) | 文件类型 · 可空 |
| `status` | varchar(8) | 状态 · 可空 |
| `result_msg` | varchar(256) | 结果描述 · 可空 |
| `remark` | varchar(64) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
