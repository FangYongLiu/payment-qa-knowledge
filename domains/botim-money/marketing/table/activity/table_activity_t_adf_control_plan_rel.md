---
id: tbl_activity_t_adf_control_plan_rel
object_type: Table
name: 券定义与发券控制方案关联表#记录券定义与发券控制方案的关联关系#新增券定义或要调整券定义的发券控制方案时要新增或修改记录#yanghuilong (t_adf_control_plan_rel)
aliases: [t_adf_control_plan_rel, activity.t_adf_control_plan_rel]
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

# 券定义与发券控制方案关联表#记录券定义与发券控制方案的关联关系#新增券定义或要调整券定义的发券控制方案时要新增或修改记录#yanghuilong (t_adf_control_plan_rel)

## 用途
物理表 `activity.t_adf_control_plan_rel`,主键 `None`。券定义与发券控制方案关联表#记录券定义与发券控制方案的关联关系#新增券定义或要调整券定义的发券控制方案时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `award_define_id` | int | 待补 |
| `control_plan_id` | int | 发券控制方案id |

## 主键 / 索引
- 主键:`None`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
