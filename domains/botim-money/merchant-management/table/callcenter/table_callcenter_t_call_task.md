---
id: tbl_callcenter_t_call_task
object_type: Table
name: 单个的呼叫任务表 (t_call_task)
aliases: [t_call_task, callcenter.t_call_task]
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

# 单个的呼叫任务表 (t_call_task)

## 用途
物理表 `callcenter.t_call_task`,主键 `id`。单个的呼叫任务表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `batch_no` | varchar(32) | 批次号 |
| `task_type` | smallint(4) | 待补 |
| `caller` | varchar(32) | 待补 |
| `callee` | varchar(32) | 被叫号码 |
| `retry_threshold` | smallint(4) | 重试次数阈值，如1表示只拨打1次 |
| `retry_interval_type` | smallint(4) | 重试间隔类型：0:0分钟，1：5分钟 |
| `status` | smallint(4) | 待补 |
| `call_result` | smallint(4) | 待补 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 最近一次更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_bn_callee`:batch_no, callee (UNIQUE)
- `ix_ct`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
