---
id: tbl_feature_tm_feature_info
object_type: Table
name: 功能详细表 (tm_feature_info)
aliases: [tm_feature_info, feature.tm_feature_info]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: feature schema DDL
tags: [activation, feature]
sensitivity: normal
related_services: []
---

# 功能详细表 (tm_feature_info)

## 用途
物理表 `feature.tm_feature_info`,主键 `feature_id`。功能详细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `feature_id` | int | 主键ID · 可空 |
| `feature_name` | varchar(32) | 功能名称 · 可空 |
| `feature_type` | varchar(32) | 功能类似 · 可空 |
| `feature_sub_type` | varchar(32) | 功能子类 · 可空 |
| `feature_status` | varchar(32) | 功能状态 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`feature_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
