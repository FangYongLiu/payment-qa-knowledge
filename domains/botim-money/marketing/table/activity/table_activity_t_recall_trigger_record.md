---
id: tbl_activity_t_recall_trigger_record
object_type: Table
name: 营销活动产生的触达记录表#记录营销活动的触达记录#营销活动执行产生触达任务或触达执行时时要新增或更新此表#yanghuilong (t_recall_trigger_record)
aliases: [t_recall_trigger_record, activity.t_recall_trigger_record]
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

# 营销活动产生的触达记录表#记录营销活动的触达记录#营销活动执行产生触达任务或触达执行时时要新增或更新此表#yanghuilong (t_recall_trigger_record)

## 用途
物理表 `activity.t_recall_trigger_record`,主键 `id`。营销活动产生的触达记录表#记录营销活动的触达记录#营销活动执行产生触达任务或触达执行时时要新增或更新此表#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | id · 可空 |
| `recall_plan_id` | int(10) | 召回计划id |
| `member_id` | bigint(32) | 用户id |
| `status` | smallint(4) | 待补 |
| `award_record_id` | int(10) | 券id · 可空 |
| `notify_record_id` | int(10) | 发出通知的id，对应t_notify_record表的id · 可空 |
| `page_record_id` | int(10) | 开屏页记录id · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 最近一次更新时间 |
| `valid_period` | int | 有效时间，过期不再处理。单位s |
| `memo` | varchar(128) | 记录放弃执行的原因 · 可空 |

## 主键 / 索引
- 主键:`id`
- `ix_recall_plan`:recall_plan_id, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
