---
id: tbl_remittance_t_dyn_quote_log
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_dyn_quote_log
subdomain: remittance
module: null
sensitivity: normal
name: t_dyn_quote_log
aliases:
- t_dyn_quote_log
related_services:
- svc_remittance
related_scenarios: []
---
# t_dyn_quote_log

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | —(DDL未定义) |  |  |
| `member_id` | —(DDL未定义) |  |  |
| `strategy_id` | —(DDL未定义) |  |  |
| `event_code` | —(DDL未定义) |  |  |
| `send_amount` | —(DDL未定义) |  |  |
| `receive_country` | —(DDL未定义) |  |  |
| `channel_code` | —(DDL未定义) |  |  |
| `action_type` | —(DDL未定义) |  |  |
| `action_result` | —(DDL未定义) |  |  |
| `matched_rule_ids` | —(DDL未定义) |  |  |
| `latency_ms` | —(DDL未定义) |  |  |
| `gmt_create` | —(DDL未定义) |  |  |

## 主键 / 索引
- 主键:(待补)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
