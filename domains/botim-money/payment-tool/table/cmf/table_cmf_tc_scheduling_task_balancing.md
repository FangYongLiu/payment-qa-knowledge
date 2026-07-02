---
id: tbl_cmf_tc_scheduling_task_balancing
object_type: Table
name: tc_scheduling_task_balancing (tc_scheduling_task_balancing)
aliases: [tc_scheduling_task_balancing, cmf.tc_scheduling_task_balancing]
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

# tc_scheduling_task_balancing (tc_scheduling_task_balancing)

## 用途
物理表 `cmf.tc_scheduling_task_balancing`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | decimal(11) | ID |
| `TASK_NAME` | varchar(64) | 任务名称 · 可空 |
| `TASK_DESCRIPTION` | varchar(64) | 任务描述 · 可空 |
| `REDUCE_SIZE` | decimal | 任务分解大小 · 可空 |
| `REDUCE_MODE` | char | 分解方式,F（fore）预先的；T(temp)临时的 · 可空 |
| `TASK_FAILURE` | decimal | 任务失效时间,即总任务执行失败时间,单位分钟 · 可空 |
| `REDUCE_FAILURE` | decimal | 分解失效时间,即分解后的任务执行失败时间,单位分钟 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
