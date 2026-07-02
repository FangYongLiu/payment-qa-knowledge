---
id: tbl_offlinepay_t_command_param
object_type: Table
name: command param (t_command_param)
aliases: [t_command_param, offlinepay.t_command_param]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# command param (t_command_param)

## 用途
物理表 `offlinepay.t_command_param`,主键 `id, pkey`。command param。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | command id |
| `pkey` | varchar(50) | param key |
| `value` | varchar(200) | param value |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
