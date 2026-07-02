---
id: tbl_payment_tb_daemon_task_trigger
object_type: Table
name: 定时任务触发器 (tb_daemon_task_trigger)
aliases: [tb_daemon_task_trigger, payment.tb_daemon_task_trigger]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 定时任务触发器 (tb_daemon_task_trigger)

## 用途
物理表 `payment.tb_daemon_task_trigger`,主键 `TRIGGER_ID`。定时任务触发器。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TRIGGER_ID` | decimal(11) | 主键seq:SEQ_DAEMON_TASK_TRIGGER |
| `DESCRIPTION` | varchar(64) | 描述 |
| `TASK_TYPE` | varchar(64) | 任务类型 |
| `CRON_EXPRESSION` | varchar(32) | 定时表达式 |
| `GMT_START` | timestamp | 开始时间 · 可空 |
| `GMT_END` | timestamp | 结束时间 · 可空 |
| `GMT_PREVIOUS_FIRE` | timestamp | 上次执行时间 · 可空 |
| `GMT_NEXT_FIRE` | timestamp | 下次执行时间 · 可空 |
| `STATUS` | char | 状态：Y已启用；N未启用；P暂停 |
| `EXECUTE_STATUS` | char | 执行状态：E执行中；F执行结束； |
| `CONCURRENT_TAG` | char | 并发标志：Y-需要并发控制；N-不需要并发控制 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`TRIGGER_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
