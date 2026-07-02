---
id: tbl_collection_sys_dict
object_type: Table
name: 数据字典 (sys_dict)
aliases: [sys_dict, collection.sys_dict]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 数据字典 (sys_dict)

## 用途
物理表 `collection.sys_dict`,主键 `dict_id`。数据字典。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dict_id` | bigint | ID · 可空 |
| `name` | varchar(255) | 字典名称 |
| `description` | varchar(255) | 描述 · 可空 |
| `create_by` | varchar(255) | 创建者 · 可空 |
| `update_by` | varchar(255) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`dict_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
