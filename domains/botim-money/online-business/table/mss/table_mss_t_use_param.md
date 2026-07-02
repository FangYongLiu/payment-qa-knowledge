---
id: tbl_mss_t_use_param
object_type: Table
name: 用户工具使用配置 (t_use_param)
aliases: [t_use_param, mss.t_use_param]
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

# 用户工具使用配置 (t_use_param)

## 用途
物理表 `mss.t_use_param`,主键 `id`。用户工具使用配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `tool_id` | int | 工具id |
| `param_type` | varchar(64) | 活动code |
| `param_key` | varchar(64) | 活动名称 |
| `param_value` | varchar(256) | 活动类型 |
| `compare_method` | varchar(16) | 活动子类型 默认default |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
