---
id: tbl_payment_tb_machine_monitor
object_type: Table
name: 机器监控信息 (tb_machine_monitor)
aliases: [tb_machine_monitor, payment.tb_machine_monitor]
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

# 机器监控信息 (tb_machine_monitor)

## 用途
物理表 `payment.tb_machine_monitor`,主键 `ID`。机器监控信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | decimal(11) | pk |
| `MACHINE_IP` | varchar(32) | 机器IP |
| `MACHINE_NAME` | varchar(32) | 机器名称 · 可空 |
| `TASK_TYPE` | varchar(32) | 任务类型。C：缓存任务；T：触发器???务 · 可空 |
| `TASK_KEY` | varchar(32) | 任务键值 · 可空 |
| `TASK_PARAM` | varchar(64) | 任务参数 · 可空 |
| `NEED_FRESH` | char | 是否需要刷新。Y：需要 N：不需要 · 可空 |
| `GMT_REFRESH` | timestamp | 刷新时间 · 可空 |
| `GMT_REGISTER` | timestamp | 最新注册时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`ID`
- `IDX_MM_MACHINE_IP`:MACHINE_IP
- `IDX_MM_MACHINE_NAME`:MACHINE_NAME

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
