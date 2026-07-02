---
id: tbl_basisportal_t_ru_variable
object_type: Table
name: variables in instance (t_ru_variable)
aliases: [t_ru_variable, basisportal.t_ru_variable]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# variables in instance (t_ru_variable)

## 用途
物理表 `basisportal.t_ru_variable`,主键 `id`。variables in instance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `instance_id` | bigint(21) | instance ID |
| `name` | varchar(100) | variable name |
| `value` | varchar(512) | variable value · 可空 |
| `task_key` | varbinary(32) | task key · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
