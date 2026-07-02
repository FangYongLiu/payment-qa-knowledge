---
id: tbl_counter_t_audit_log
object_type: Table
name: 审核日志表 (t_audit_log)
aliases: [t_audit_log, counter.t_audit_log]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 审核日志表 (t_audit_log)

## 用途
物理表 `counter.t_audit_log`,主键 `log_id`。审核日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint(17) | 日志ID |
| `audit_id` | bigint(17) | 审核记录ID · 可空 |
| `audit_type` | varchar(16) | 审核类型  · 可空 |
| `pre_status` | varchar(16) | 审核前状态 · 可空 |
| `status` | varchar(16) | 当前状态 A-审核中 D-审核拒绝 P-审核通过  · 可空 |
| `operator` | varchar(32) | 操作者 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `log_type` | varchar(16) | 日志类型 S-系统日志 O-操作者日志 · 可空 |
| `ip` | varchar(32) | ip · 可空 |

## 主键 / 索引
- 主键:`log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
