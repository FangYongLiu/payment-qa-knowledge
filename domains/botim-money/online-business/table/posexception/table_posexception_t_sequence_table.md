---
id: tbl_posexception_t_sequence_table
object_type: Table
name: 序号生成表 (t_sequence_table)
aliases: [t_sequence_table, posexception.t_sequence_table]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: posexception schema DDL
tags: [online-business, posexception]
sensitivity: normal
related_services: [svc_pos_exception_processor]
---

# 序号生成表 (t_sequence_table)

## 用途
物理表 `posexception.t_sequence_table`,主键 `sequence_name`。序号生成表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sequence_name` | varchar(128) | 序列名称 |
| `sequence_value` | bigint | 序列值 |

## 主键 / 索引
- 主键:`sequence_name`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
