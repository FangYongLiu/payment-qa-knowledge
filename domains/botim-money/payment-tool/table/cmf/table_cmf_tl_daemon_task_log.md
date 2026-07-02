---
id: tbl_cmf_tl_daemon_task_log
object_type: Table
name: 任务执行日志 (tl_daemon_task_log)
aliases: [tl_daemon_task_log, cmf.tl_daemon_task_log]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 任务执行日志 (tl_daemon_task_log)

## 用途
物理表 `cmf.tl_daemon_task_log`,主键 `TASK_LOG_ID`。任务执行日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TASK_LOG_ID` | decimal(19) | SEQ:SEQ_DAEMON_TASK_LOG |
| `TRIGGER_ID` | decimal(11) | 触发ID |
| `DESCRIPTION` | varchar(64) | 描述 |
| `GMT_NEXT_FIRE` | timestamp | 下次触发时间 · 可空 |
| `MACHINE_NAME` | varchar(32) | 机器名称 · 可空 |
| `MACHINE_IP` | varchar(32) | 机器IP |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`TASK_LOG_ID`
- `IDX_DTL_TRIGGER_ID`:TRIGGER_ID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
