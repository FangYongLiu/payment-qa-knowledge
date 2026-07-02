---
id: tbl_activity_t_business_scene
object_type: Table
name: 业务场景表#记录业务场景的定义#新增业务场景时使用此表#yanghuilong (t_business_scene)
aliases: [t_business_scene, activity.t_business_scene]
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

# 业务场景表#记录业务场景的定义#新增业务场景时使用此表#yanghuilong (t_business_scene)

## 用途
物理表 `activity.t_business_scene`,主键 `id`。业务场景表#记录业务场景的定义#新增业务场景时使用此表#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Id · 可空 |
| `business_scene_code` | varchar(128) | 业务场景的编码或英文名 |
| `business_scene_name` | varchar(255) | 业务场景名称 · 可空 |
| `condition_ids` | varchar(255) | 关联的条件id，以逗号分隔，条件间为且的关系 · 可空 |
| `status` | smallint(4) | 状态，1：生效，2：失效 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 最近一次更新时间 |

## 主键 / 索引
- 主键:`id`
- `ix_code`:business_scene_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
