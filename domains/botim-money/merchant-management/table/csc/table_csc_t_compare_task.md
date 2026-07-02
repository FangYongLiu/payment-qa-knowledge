---
id: tbl_csc_t_compare_task
object_type: Table
name: 对账任务 (t_compare_task)
aliases: [t_compare_task, csc.t_compare_task]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 对账任务 (t_compare_task)

## 用途
物理表 `csc.t_compare_task`,主键 `task_id`。对账任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `task_id` | bigint | 任务ID · 可空 |
| `define_id` | bigint | 定义ID |
| `task_type` | char | 任务类型：M=人工，S=计划，R=重试 |
| `operator` | varchar(64) | 操作员 |
| `orig_task_id` | bigint | 原任务ID · 可空 |
| `data_begin_time` | timestamp | 数据开始时间 |
| `data_end_time` | timestamp | 数据结束时间 |
| `task_status` | varchar(10) | 任务状态：P=处理中，S=一致，F=不一致，CP=补单中，RW=等待重试，RS=重试成功 |
| `compare_statistic` | varchar(128) | 对账统计 · 可空 |
| `error_code` | varchar(32) | 错误码 · 可空 |
| `error_message` | varchar(255) | 错误信息 · 可空 |
| `last_retry_task_id` | bigint | 最后重试任务ID · 可空 |
| `compare_consume` | int | 对账耗时：单位：秒 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`task_id`
- `idx_createtime_taskstatus`:create_time, task_status
- `idx_orig_task_id`:orig_task_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
