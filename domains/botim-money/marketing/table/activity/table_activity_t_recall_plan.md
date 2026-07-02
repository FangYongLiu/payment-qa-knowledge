---
id: tbl_activity_t_recall_plan
object_type: Table
name: 营销活动计划表#记录营销活动#新增或要修改营销活动时要新增或更新此表#yanghuilong (t_recall_plan)
aliases: [t_recall_plan, activity.t_recall_plan]
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

# 营销活动计划表#记录营销活动#新增或要修改营销活动时要新增或更新此表#yanghuilong (t_recall_plan)

## 用途
物理表 `activity.t_recall_plan`,主键 `id`。营销活动计划表#记录营销活动#新增或要修改营销活动时要新增或更新此表#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | id · 可空 |
| `plan_code` | varchar(128) | 召回方案编码 |
| `plan_des` | varchar(255) | 方案描述 · 可空 |
| `plan_group` | varchar(128) | 活动所属活动组 |
| `execute_type` | smallint(4) | 执行方式：1：定时执行，2：手动执行 |
| `user_group_id` | int(10) | 活动目标用户群体id |
| `notify_plan_id` | int(10) | 通知方案id · 可空 |
| `award_define_id` | int | 券定义id · 可空 |
| `page_define_id` | int(10) | 开屏页定义id · 可空 |
| `cron` | varchar(128) | 定时 · 可空 |
| `product` | smallint(4) | 产品，1、cashnow，2、paylater，3、wecredit |
| `start_time` | timestamp | 有效期开始时间 |
| `end_time` | timestamp | 有效期结束时间 |
| `status` | smallint(4) | 状态，1：生效，2：失效 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_code`:plan_code (UNIQUE)
- `ix_c_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
