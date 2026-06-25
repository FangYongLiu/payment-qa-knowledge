---
id: tbl_fundout_tt_daemon_task_trigger
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_daemon_task_trigger
subdomain: fundout
module: null
sensitivity: normal
name: 定时任务触发器(tt_daemon_task_trigger)
aliases:
- tt_daemon_task_trigger
related_services:
- svc_fundout
related_scenarios: []
---
# 定时任务触发器(tt_daemon_task_trigger)

## 用途
定时任务触发器。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL | 序列 |
| `TASK_TYPE` | varchar(32) | NOT NULL | 触发器类型,任务类型 |
| `CRON_EXPRESSION` | varchar(32) | NOT NULL | 时间表达式 |
| `FORCE_REFRESH` | char | NOT NULL | 是否需要强制刷新,Y:是,N:否 |
| `EXECUTE_STATUS` | char | NOT NULL | 触发器执行状态, F:执行结束,P:执行中 |
| `STATUS` | char | NOT NULL | 触发器状态, S:启动,F:暂停,C:关闭 |
| `MACHINE_IP` | varchar(32) |  | 当前定时任务的执行机器IP |
| `MACHINE_HOST` | varchar(32) |  | 当前定时任务的执行机器名 |
| `GMT_START` | timestamp |  | 触发器开始时间 |
| `GMT_END` | timestamp |  | 触发器结束时间 |
| `DESCRIPTION` | varchar(128) |  | 描述 |
| `MEMO` | varchar(64) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |
| `CONCURRENT_TAG` | char |  | 并发控制,Y,N |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `UK_DAEMON_TASK_TRIGGER_KEY` 唯一 (TASK_TYPE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
