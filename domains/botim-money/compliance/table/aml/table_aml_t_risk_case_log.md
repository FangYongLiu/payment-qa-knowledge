---
id: tbl_aml_t_risk_case_log
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
- t_risk_case_log
subdomain: aml
module: null
sensitivity: normal
name: 案件操作日志(t_risk_case_log)
aliases:
- t_risk_case_log
related_services:
- svc_aml
related_scenarios: []
---
# 案件操作日志(t_risk_case_log)

## 用途
案件操作日志。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `case_id` | bigint |  | 案件id |
| `operator` | varchar(20) |  | 操作人 |
| `before_status` | varchar(50) |  | 操作前状态 |
| `after_status` | varchar(50) |  | 操作后状态 |
| `indemnity_amount` | decimal(15,4) |  | 赔付金额 |
| `currency` | varchar(20) |  | 币种 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_case_log_case_id` (case_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
