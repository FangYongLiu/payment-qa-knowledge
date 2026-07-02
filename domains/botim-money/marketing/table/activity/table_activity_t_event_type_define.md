---
id: tbl_activity_t_event_type_define
object_type: Table
name: 事件类型定义表#记录业务可能发起的事件类型#新增事件类型或要修改已有事件类型时要新增或修改记录#yanghuilong (t_event_type_define)
aliases: [t_event_type_define, activity.t_event_type_define]
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

# 事件类型定义表#记录业务可能发起的事件类型#新增事件类型或要修改已有事件类型时要新增或修改记录#yanghuilong (t_event_type_define)

## 用途
物理表 `activity.t_event_type_define`,主键 `id`。事件类型定义表#记录业务可能发起的事件类型#新增事件类型或要修改已有事件类型时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `event_type_code` | varchar(64) | 事件类型编码 |
| `event_type_desc` | varchar(128) | 事件类型描述 · 可空 |
| `system_name` | varchar(64) | 事件类型所属系统 |
| `param_list` | varchar(255) | 事件中需要携带的参数名list，参数名之间用英文的逗号分割 · 可空 |
| `status` | smallint(4) | 1:生效，0：失效 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |
| `award_define_id` | int(10) | 关联的优惠券定义id · 可空 |
| `notify_plan_id` | int(10) | 关联的通知id · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_code`:event_type_code, system_name (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
