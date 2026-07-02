---
id: tbl_ccsales_t_command_param
object_type: Table
name: 指令参数(分区) (t_command_param)
aliases: [t_command_param, ccsales.t_command_param]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccsales schema DDL
tags: [crypto, ccsales]
sensitivity: normal
related_services: []
---

# 指令参数(分区) (t_command_param)

## 用途
物理表 `ccsales.t_command_param`,主键 `id, pkey`。指令参数(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `pkey` | varchar(50) | 键 |
| `value` | varchar(200) | 值 |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
