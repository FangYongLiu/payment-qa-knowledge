---
id: tbl_csc_t_job_progress
object_type: Table
name: 任务进度表 (t_job_progress)
aliases: [t_job_progress, csc.t_job_progress]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 任务进度表 (t_job_progress)

## 用途
物理表 `csc.t_job_progress`,主键 `job_code`。任务进度表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `job_code` | varchar(32) | 任务代码 |
| `job_desc` | varchar(32) | 任务描述 · 可空 |
| `check_minutes` | int | 检查时长 |
| `delay_minutes` | int | 延迟时长 |
| `checked_time` | timestamp | 当前进度 |
| `next_trigger_time` | timestamp | 下次触发时间 |
| `enable_flag` | char | 启用标识: Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `update_version` | bigint | 修改版本 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`job_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
