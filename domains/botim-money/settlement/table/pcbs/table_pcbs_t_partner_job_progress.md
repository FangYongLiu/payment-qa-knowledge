---
id: tbl_pcbs_t_partner_job_progress
object_type: Table
name: Partner Job Progress (t_partner_job_progress)
aliases: [t_partner_job_progress, pcbs.t_partner_job_progress]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Partner Job Progress (t_partner_job_progress)

## 用途
物理表 `pcbs.t_partner_job_progress`,主键 `progress_id`。Partner Job Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `progress_id` | bigint | Progress ID · 可空 |
| `partner_id` | varchar(20) | Partner ID |
| `job_code` | varchar(32) | Job Code |
| `job_progress` | varchar(32) | Job Progress |
| `enable_flag` | char | Enable Flag: Y=Yes, N=No |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`progress_id`
- `uk_partner_id_job_code`:partner_id, job_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
