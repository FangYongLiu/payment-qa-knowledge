---
id: tbl_benefit_t_task_statistic
object_type: Table
name: t_task_statistic (t_task_statistic)
aliases: [t_task_statistic, benefit.t_task_statistic]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_task_statistic (t_task_statistic)

## 用途
物理表 `benefit.t_task_statistic`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键自增 · 可空 |
| `task_code` | varchar(50) | 任务代码 |
| `total_items` | int | 总数 |
| `executed_items` | int | 执行数 · 可空 |
| `task_flag` | varchar(20) | 任务标记。完成：COMPLETED · 可空 |
| `statistic_date` | date | 统计日期 · 可空 |
| `task_start_time` | timestamp | 任务开始时间 · 可空 |
| `task_end_time` | timestamp | 任务结束时间 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_code_date`:task_code, statistic_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
