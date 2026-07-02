---
id: tbl_marketnotify_t_market_task
object_type: Table
name: 调度任务 (t_market_task)
aliases: [t_market_task, marketnotify.t_market_task]
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

# 调度任务 (t_market_task)

## 用途
物理表 `marketnotify.t_market_task`,主键 `id`。调度任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `job_code` | varchar(32) | 调度code |
| `target_source` | varchar(64) | 目标表 |
| `status` | varchar(32) | 任务状态：PROCESS=处理中,PAUSE=暂停,SUCCESS=成功,FAIL=失败 |
| `begin_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `exec_count` | bigint | 处理条数 · 可空 |
| `error_msg` | varchar(255) | 错误信息 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
