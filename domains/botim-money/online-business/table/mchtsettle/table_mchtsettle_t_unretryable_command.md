---
id: tbl_mchtsettle_t_unretryable_command
object_type: Table
name: unretryable command (t_unretryable_command)
aliases: [t_unretryable_command, mchtsettle.t_unretryable_command]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# unretryable command (t_unretryable_command)

## 用途
物理表 `mchtsettle.t_unretryable_command`,主键 `id`。unretryable command。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `parent_type` | varchar(50) | order type |
| `parent_id` | bigint | order id |
| `command` | varchar(50) | command |

## 主键 / 索引
- 主键:`id`
- `uk_urcmd_prt`:parent_id, parent_type, command (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
