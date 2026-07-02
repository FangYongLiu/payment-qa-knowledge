---
id: tbl_ups_t_ups_user_contacts_key
object_type: Table
name: 通讯录key (t_ups_user_contacts_key)
aliases: [t_ups_user_contacts_key, ups.t_ups_user_contacts_key]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 通讯录key (t_ups_user_contacts_key)

## 用途
物理表 `ups.t_ups_user_contacts_key`,主键 `id`。通讯录key。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `contacts_key` | varchar(32) | 通讯录key |
| `start_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
