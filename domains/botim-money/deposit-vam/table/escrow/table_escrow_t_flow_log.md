---
id: tbl_escrow_t_flow_log
object_type: Table
name: 流水日志表 (t_flow_log)
aliases: [t_flow_log, escrow.t_flow_log]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 流水日志表 (t_flow_log)

## 用途
物理表 `escrow.t_flow_log`,主键 `log_id`。流水日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint(19) | 日志id |
| `batch_id` | bigint(19) | 批处理号 · 可空 |
| `handle_type` | varchar(4) | 处理类型 · 可空 |
| `next_step` | varchar(32) | 下一步操作 · 可空 |
| `status` | varchar(4) | 此步骤处理状态 · 可空 |
| `start_time` | timestamp | 起始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `memo` | varchar(512) | memo · 可空 |

## 主键 / 索引
- 主键:`log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
