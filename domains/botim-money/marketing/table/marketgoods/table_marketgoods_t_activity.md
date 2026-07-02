---
id: tbl_marketgoods_t_activity
object_type: Table
name: 活动表 (t_activity)
aliases: [t_activity, marketgoods.t_activity]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketgoods schema DDL
tags: [marketing, marketgoods]
sensitivity: normal
related_services: []
---

# 活动表 (t_activity)

## 用途
物理表 `marketgoods.t_activity`,主键 `id`。活动表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `activity_code` | varchar(16) | 活动编号 |
| `activity_title` | varchar(100) | 活动标题 |
| `activity_url` | varchar(200) | 活动链接 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `pk_activity_code`:activity_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
