---
id: tbl_mss_t_marketing_activity
object_type: Table
name: 活动定义 (t_marketing_activity)
aliases: [t_marketing_activity, mss.t_marketing_activity]
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

# 活动定义 (t_marketing_activity)

## 用途
物理表 `mss.t_marketing_activity`,主键 `activity_id`。活动定义。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `activity_id` | int | 主键id · 可空 |
| `activity_code` | varchar(64) | 活动code |
| `activity_name` | varchar(64) | 活动名称 |
| `activity_type` | varchar(16) | 活动类型 |
| `activity_sub_type` | varchar(64) | 活动子类型 默认default |
| `default_invite` | char | 受邀活动 y,n |
| `whitelist_key` | varchar(32) | 白名单key · 可空 |
| `status` | char | 状态 y,n |
| `event_url` | varchar(256) | 活动url · 可空 |
| `resource_url` | varchar(256) | 活动资源url · 可空 |
| `utm_source` | varchar(32) | utm_source · 可空 |
| `priority` | int | 优先级 · 可空 |
| `start_time` | timestamp | 活动开始时间 |
| `end_time` | timestamp | 活动结束时间 |
| `memo` | varchar(64) | 活动备注 · 可空 |
| `rule_hook` | varchar(32) | 规则钩子 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`activity_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
