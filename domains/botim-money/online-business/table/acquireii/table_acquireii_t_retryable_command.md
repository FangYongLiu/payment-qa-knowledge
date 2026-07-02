---
id: tbl_acquireii_t_retryable_command
object_type: Table
name: 可重试指令表 (t_retryable_command)
aliases: [t_retryable_command, acquireii.t_retryable_command]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# 可重试指令表 (t_retryable_command)

## 用途
物理表 `acquireii.t_retryable_command`,主键 `id`。可重试指令(分区)。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
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
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
