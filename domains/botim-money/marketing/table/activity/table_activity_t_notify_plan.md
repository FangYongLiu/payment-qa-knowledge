---
id: tbl_activity_t_notify_plan
object_type: Table
name: 通知方案表#记录通知方案#新增方案或要修改已有方案时要新增或修改记录#yanghuilong (t_notify_plan)
aliases: [t_notify_plan, activity.t_notify_plan]
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

# 通知方案表#记录通知方案#新增方案或要修改已有方案时要新增或修改记录#yanghuilong (t_notify_plan)

## 用途
物理表 `activity.t_notify_plan`,主键 `id`。通知方案表#记录通知方案#新增方案或要修改已有方案时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `plan_name` | varchar(128) | 通知方案名称 |
| `description` | varchar(128) | 通知方案描述 · 可空 |
| `status` | smallint(4) | 状态：1.生效2.失效 |
| `msg_type` | smallint(4) | 通知内容 的类型：1：纯文本正文，只看content字段，2、纯文本 标题+正文，关注title,content两个字段,3、HTML 标题+正文，同t_msg_template中的msg_type |
| `inform_way` | smallint(4) | 通知方式：1：短信、2、app站内信 |
| `inform_channel` | smallint(4) | 通知渠道：1：短信、2：cashnow native app、3：botim、4：totok、5：payby |
| `notify_app_flag` | smallint(4) | 待补 |
| `product` | smallint(4) | 1、cashnow，2、paylater，3、wecredit |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `msg_template_id` | int | 消息模版id |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
