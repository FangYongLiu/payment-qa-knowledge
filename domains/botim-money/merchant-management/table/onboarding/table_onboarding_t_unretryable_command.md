---
id: tbl_onboarding_t_unretryable_command
object_type: Table
name: unretryable_command (t_unretryable_command)
aliases: [t_unretryable_command, onboarding.t_unretryable_command]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# unretryable_command (t_unretryable_command)

## 用途
物理表 `onboarding.t_unretryable_command`,主键 `id`。unretryable_command。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `parent_type` | varchar(50) | parent_type |
| `parent_id` | bigint | parent_id |
| `command` | varchar(50) | command |

## 主键 / 索引
- 主键:`id`
- `uk_urcmd_prt`:parent_id, parent_type, command (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
