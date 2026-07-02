---
id: tbl_ccceth_t_retryable_command
object_type: Table
name: 可重试指令(分区) (t_retryable_command)
aliases: [t_retryable_command, ccceth.t_retryable_command]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccceth schema DDL
tags: [crypto, ccceth]
sensitivity: normal
related_services: []
---

# 可重试指令(分区) (t_retryable_command)

## 用途
物理表 `ccceth.t_retryable_command`,主键 `id`。可重试指令(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `parent_type` | varchar(50) | 订单类型 |
| `parent_id` | bigint | 订单id |
| `command` | varchar(50) | 指令 |

## 主键 / 索引
- 主键:`id`
- `i_rcmd_prt`:parent_id, parent_type, command

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
