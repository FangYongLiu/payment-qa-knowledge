---
id: tbl_callcenter_t_call_record
object_type: Table
name: 队列呼叫记录 (t_call_record)
aliases: [t_call_record, callcenter.t_call_record]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: callcenter schema DDL
tags: [merchant-management, callcenter]
sensitivity: normal
related_services: []
---

# 队列呼叫记录 (t_call_record)

## 用途
物理表 `callcenter.t_call_record`,主键 `id`。队列呼叫记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `task_id` | int | 任务id，对应t_call_task 的id字段 |
| `ext_num` | varchar(32) | 队列呼叫时接听的分机号 · 可空 |
| `status` | smallint(4) | 待补 |
| `call_result` | smallint(4) | 待补 · 可空 |
| `call_id` | varchar(32) | pbx返回的呼叫id · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 最近一次更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_cid`:call_id (UNIQUE)
- `ix_ct`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
