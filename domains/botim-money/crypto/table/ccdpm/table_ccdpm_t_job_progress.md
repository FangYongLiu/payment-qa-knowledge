---
id: tbl_ccdpm_t_job_progress
object_type: Table
name: 任务进度 (t_job_progress)
aliases: [t_job_progress, ccdpm.t_job_progress]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 任务进度 (t_job_progress)

## 用途
物理表 `ccdpm.t_job_progress`,主键 `job_code`。任务进度。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `job_code` | varchar(128) | 任务代码 |
| `job_desc` | varchar(1024) | 任务描述 |
| `job_progress` | varchar(128) | 任务进度 |
| `extension` | varchar(1024) | 扩展参数 · 可空 |
| `memo` | varchar(1024) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`job_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
