---
id: tbl_cmf_tt_distributed_lock
object_type: Table
name: tt_distributed_lock (tt_distributed_lock)
aliases: [tt_distributed_lock, cmf.tt_distributed_lock]
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

# tt_distributed_lock (tt_distributed_lock)

## 用途
物理表 `cmf.tt_distributed_lock`,主键 `LOCK_TICKET`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LOCK_TICKET` | varchar(128) | 标识,锁的唯一区别码 |
| `LOCK_NAME` | varchar(64) | 锁名称 · 可空 |
| `LOCK_TYPE` | char | 锁类型：E排它锁,S同步锁 |
| `LOCK_DESC` | varchar(100) | 描述 · 可空 |
| `LOCK_STATUS` | char | 锁状态,E执行中；F执行结束； · 可空 |
| `GMT_LOCK` | timestamp | 上锁时间 · 可空 |
| `MACHINE_IP` | varchar(32) | 加锁机器IP · 可空 |
| `MACHINE_HOST` | varchar(32) | 加锁机器HOST · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`LOCK_TICKET`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
