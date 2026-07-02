---
id: tbl_activity_t_user_group
object_type: Table
name: 符合一定条件的用户群定义表#记录用户群定义#新增或要修改用户群体时要新增或更新此表#yanghuilong (t_user_group)
aliases: [t_user_group, activity.t_user_group]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# 符合一定条件的用户群定义表#记录用户群定义#新增或要修改用户群体时要新增或更新此表#yanghuilong (t_user_group)

## 用途
物理表 `activity.t_user_group`,主键 `id`。符合一定条件的用户群定义表#记录用户群定义#新增或要修改用户群体时要新增或更新此表#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `user_group_code` | varchar(128) | 待补 |
| `user_group_name` | varchar(255) | 用户群的名称 · 可空 |
| `condition_ids` | varchar(255) | 关联的条件id列表,以逗号分隔,条件间为且的关系 · 可空 |
| `query_sql` | varchar(4896) | 筛选sql · 可空 |
| `status` | smallint(4) | 状态：1：生效，2：失效 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 最近更新时间 |

## 主键 / 索引
- 主键:`id`
- `ix_code`:user_group_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
