---
id: tbl_aml_t_search_log
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_search_log
subdomain: aml
module: null
sensitivity: normal
name: 搜索日志表(t_search_log)
aliases:
- t_search_log
related_services:
- svc_aml
related_scenarios: []
---
# 搜索日志表(t_search_log)

## 用途
搜索日志表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `search_type` | varchar(16) | 默认 '' | 扫描类型：kyc、payment |
| `biz_id` | varchar(32) | 默认 '' | 业务ID |
| `search_content` | json |  | 搜索内容 |
| `search_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 查询时间 |
| `result_id` | bigint |  | resultId |
| `status` | int | 默认 0 | 状态：0.默认，未扫描；1.已扫描； |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_biz_id` (biz_id)
  - `idx_result_id` (result_id)
  - `idx_search_time` (search_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
