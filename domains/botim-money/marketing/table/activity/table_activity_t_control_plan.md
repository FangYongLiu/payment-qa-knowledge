---
id: tbl_activity_t_control_plan
object_type: Table
name: 发券控制方案表#记录发券控制策略#新增发券控制策略或要调整当前已有的策略时要新增或修改记录#yanghuilong (t_control_plan)
aliases: [t_control_plan, activity.t_control_plan]
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

# 发券控制方案表#记录发券控制策略#新增发券控制策略或要调整当前已有的策略时要新增或修改记录#yanghuilong (t_control_plan)

## 用途
物理表 `activity.t_control_plan`,主键 `id`。发券控制方案表#记录发券控制策略#新增发券控制策略或要调整当前已有的策略时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id |
| `plan_name` | varchar(128) | 方案名称 |
| `total_quantity` | int | 总数量 · 可空 |
| `total_amount` | int | 总金额 · 可空 |
| `per_member_quantity` | int | 每个用户限制的数量 · 可空 |
| `per_member_amount` | int | 每个用户限制的金额 · 可空 |
| `control_granularity` | smallint(4) | 控制粒度：如0:all、1:每天、2:每月等。含义为每天**的金额或数量不超过** |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
