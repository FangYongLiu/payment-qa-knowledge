---
id: tbl_activity_job_status_trace_log
object_type: Table
name: elasticjob 定时任务运行状态记录表#用于记录的是定时任务的执行的状态日志#每次任务启动、执行、执行结束时会插入数据#yanghuilong (job_status_trace_log)
aliases: [job_status_trace_log, activity.job_status_trace_log]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# elasticjob 定时任务运行状态记录表#用于记录的是定时任务的执行的状态日志#每次任务启动、执行、执行结束时会插入数据#yanghuilong (job_status_trace_log)

## 用途
物理表 `activity.job_status_trace_log`,主键 `id`。elasticjob 定时任务运行状态记录表#用于记录的是定时任务的执行的状态日志#每次任务启动、执行、执行结束时会插入数据#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(40) | 待补 |
| `job_name` | varchar(128) | 待补 |
| `original_task_id` | varchar(128) | 待补 |
| `task_id` | varchar(128) | 待补 |
| `slave_id` | varchar(50) | 执行作业服务器的名称，Lite版本为服务器的IP地址，Cloud版本为Mesos执行机主键 |
| `source` | varchar(50) | 任务执行源，可选值为CLOUD_SCHEDULER, CLOUD_EXECUTOR, LITE_EXECUTOR |
| `execution_type` | varchar(20) | 待补 |
| `sharding_item` | varchar(100) | 分片项集合，多个分片项以逗号分隔 |
| `state` | varchar(20) | 任务执行状态，可选值为TASK_STAGING, TASK_RUNNING, TASK_FINISHED, TASK_KILLED, TASK_LOST, TASK_FAILED, TASK_ERROR |
| `message` | varchar(255) | 待补 · 可空 |
| `creation_time` | timestamp | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `TASK_ID_STATE_INDEX`:task_id, state

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
