---
id: tbl_cmf_tt_scheduling_balancing_log
object_type: Table
name: tt_scheduling_balancing_log (tt_scheduling_balancing_log)
aliases: [tt_scheduling_balancing_log, cmf.tt_scheduling_balancing_log]
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

# tt_scheduling_balancing_log (tt_scheduling_balancing_log)

## 用途
物理表 `cmf.tt_scheduling_balancing_log`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | decimal(15) | ID |
| `PID` | decimal(15) | 父任务ID · 可空 |
| `BAL_ID` | decimal(11) | 负载ID · 可空 |
| `TASK_TICKET` | varchar(64) | 任务标识 可作为锁凭证 · 可空 |
| `TASK_NAME` | varchar(64) | 任务名称 · 可空 |
| `TASK_SIZE` | decimal | 任务数 · 可空 |
| `REDUCE_TYPE_SIZE` | decimal | 分解类型标识,任务大类数,即大类数 · 可空 |
| `REDUCE_SIZE` | decimal | 可分解数 · 可空 |
| `REDUCED_SIZE` | decimal | 已分解数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `STATUS` | char | 状态：R运行中；F已完成 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
