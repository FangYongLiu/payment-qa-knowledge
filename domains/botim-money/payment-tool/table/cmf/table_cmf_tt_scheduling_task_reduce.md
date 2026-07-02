---
id: tbl_cmf_tt_scheduling_task_reduce
object_type: Table
name: tt_scheduling_task_reduce (tt_scheduling_task_reduce)
aliases: [tt_scheduling_task_reduce, cmf.tt_scheduling_task_reduce]
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

# tt_scheduling_task_reduce (tt_scheduling_task_reduce)

## 用途
物理表 `cmf.tt_scheduling_task_reduce`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | decimal(15) | ID |
| `WORKER_ID` | varchar(64) | 凭证,线程或服务器分类 · 可空 |
| `REDUCE_TICKET` | varchar(64) | 分解类型标识,任务大类标识 · 可空 |
| `SCOPE_START` | varchar(64) | 目标分解头,范围的开始值 · 可空 |
| `SCOPE_END` | varchar(64) | 目标分解尾,范围的结束值 · 可空 |
| `REDUCE_SIZE` | decimal | 分配任务数 · 可空 |
| `STATUS` | char | 状态：I初始态；R运行态；E终止态; F失效 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `BAL_ID` | decimal(15) | 负载记录ID · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
