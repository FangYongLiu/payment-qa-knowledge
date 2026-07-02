---
id: tbl_marketnotify_t_market_job
object_type: Table
name: 营销活动调度 (t_market_job)
aliases: [t_market_job, marketnotify.t_market_job]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketnotify schema DDL
tags: [marketing, marketnotify]
sensitivity: normal
related_services: []
---

# 营销活动调度 (t_market_job)

## 用途
物理表 `marketnotify.t_market_job`,主键 `id`。营销活动调度。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `job_code` | varchar(32) | 任务编码：调度编码 |
| `job_strategy` | varchar(32) | 任务处理策略：处理策略 |
| `tps` | int | TPS：流量控制 · 可空 |
| `cron_express` | varchar(32) | 调度计划：调度表达式 · 可空 |
| `next_exec_time` | timestamp | 下次触发时间：下次触发时间 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(2048) | 扩展参数：json格式参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_job_code`:job_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
