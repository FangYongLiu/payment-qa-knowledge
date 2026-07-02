---
id: tbl_memberfront_t_operator_log
object_type: Table
name: 操作日志表 (t_operator_log)
aliases: [t_operator_log, memberfront.t_operator_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# 操作日志表 (t_operator_log)

## 用途
物理表 `memberfront.t_operator_log`,主键 `id`。操作日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | 主键 |
| `apply_id` | varchar(32) | 申请id |
| `op_type` | varchar(32) | 操作类型 · 可空 |
| `op_name` | varchar(50) | 操作人 · 可空 |
| `result_code` | varchar(55) | 操作结果code · 可空 |
| `result_msg` | varchar(1500) | 操作结果msg · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
