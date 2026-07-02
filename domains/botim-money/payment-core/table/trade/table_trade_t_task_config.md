---
id: tbl_trade_t_task_config
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (trade schema) 2026-06-25
tags:
- trade
- trade
- t_task_config
subdomain: trade
module: null
sensitivity: normal
name: 定时任务配置表(t_task_config)
aliases:
- t_task_config
related_services:
- svc_tradeii
related_scenarios: []
---
# 定时任务配置表(t_task_config)

## 用途
定时任务配置表。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CONFIG_ID` | varchar(32) | PK / NOT NULL | 配置ID |
| `JOB_DETAIL_NAME` | varchar(64) | NOT NULL | 任务名 |
| `CRON_EXPRESSION` | varchar(16) | NOT NULL | cron表达式 |
| `MACHINE_IP` | varchar(16) |  | 机器IP |
| `STATUS` | varchar(16) |  | 任务状态 S-启用、P-暂停、C-关闭 |
| `SUMMARY` | varchar(256) |  | 摘要 |
| `GMT_LAST` | timestamp |  | 最后执行时间 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`CONFIG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
