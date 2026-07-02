---
id: tbl_mss_t_name_list_values
object_type: Table
name: 名单内容表 (t_name_list_values)
aliases: [t_name_list_values, mss.t_name_list_values]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 名单内容表 (t_name_list_values)

## 用途
物理表 `mss.t_name_list_values`,主键 `id`。名单内容表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `value` | varchar(128) | 名单项内容 |
| `name_list_id` | bigint | 名单Id |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
