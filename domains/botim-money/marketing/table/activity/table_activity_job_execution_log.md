---
id: tbl_activity_job_execution_log
object_type: Table
name: elasticjob 定时任务记录表#用于记录的是定时任务的执行的结果日志#每次任务执行结束后会记录#yanghuilong (job_execution_log)
aliases: [job_execution_log, activity.job_execution_log]
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

# elasticjob 定时任务记录表#用于记录的是定时任务的执行的结果日志#每次任务执行结束后会记录#yanghuilong (job_execution_log)

## 用途
物理表 `activity.job_execution_log`,主键 `id`。elasticjob 定时任务记录表#用于记录的是定时任务的执行的结果日志#每次任务执行结束后会记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(40) | 待补 |
| `job_name` | varchar(128) | 待补 |
| `task_id` | varchar(128) | 任务名称,每次作业运行生成新任务 |
| `hostname` | varchar(128) | 待补 |
| `ip` | varchar(50) | 待补 |
| `sharding_item` | int | 待补 |
| `execution_source` | varchar(20) | 作业执行来源。可选值为NORMAL_TRIGGER, MISFIRE, FAILOVER |
| `failure_cause` | varchar(255) | 待补 · 可空 |
| `is_success` | tinyint(2) | 待补 |
| `start_time` | timestamp | 待补 · 可空 |
| `complete_time` | timestamp | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
