---
id: tbl_aml_t_member_risk_rate_log
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
- t_member_risk_rate_log
subdomain: aml
module: null
sensitivity: normal
name: 会员风险评级审核日志(t_member_risk_rate_log)
aliases:
- t_member_risk_rate_log
related_services:
- svc_aml
related_scenarios: []
---
# 会员风险评级审核日志(t_member_risk_rate_log)

## 用途
会员风险评级审核日志。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `rate_id` | bigint | NOT NULL | 评级id |
| `operator` | varchar(50) | NOT NULL | 操作人 |
| `remark` | varchar(200) | NOT NULL | 备注 |
| `extension` | varchar(500) | NOT NULL | 扩展字段 |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_rate_id` (rate_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
