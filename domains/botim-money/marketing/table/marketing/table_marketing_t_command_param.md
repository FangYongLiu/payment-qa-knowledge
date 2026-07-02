---
id: tbl_marketing_t_command_param
object_type: Table
name: 不可重试指令参数(分区) (t_command_param)
aliases: [t_command_param, marketing.t_command_param]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketing schema DDL
tags: [marketing, marketing]
sensitivity: normal
related_services: []
---

# 不可重试指令参数(分区) (t_command_param)

## 用途
物理表 `marketing.t_command_param`,主键 `id, pkey`。不可重试指令参数(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `pkey` | varchar(200) | 键 |
| `value` | varchar(200) | 值 |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
