---
id: tbl_aml_t_risk_merge_score
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
- t_risk_merge_score
subdomain: aml
module: null
sensitivity: normal
name: 风控合并分数表(t_risk_merge_score)
aliases:
- t_risk_merge_score
related_services:
- svc_aml
related_scenarios: []
---
# 风控合并分数表(t_risk_merge_score)

## 用途
风控合并分数表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `tid` | varchar(32) | 默认 '' | 业务ID |
| `member_id` | varchar(32) | 默认 '' | 会员ID |
| `event_type` | varchar(32) | 默认 '' | 事件类型 |
| `tmx_fraud_score` | int | 默认 0 | Tmx反欺诈风险值 |
| `aliyun_fraud_score` | int | 默认 0 | Aliyun反欺诈风险值 |
| `aliyun_aml_score` | int | 默认 0 | Aliyun反洗钱风险值 |
| `final_score` | int | 默认 0 | 最终分数 |
| `risk_status` | varchar(10) | 默认 '' | 对应风控状态：PASS/CHALLENGE/REJECT |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_create_time` (create_time)
  - `idx_tid` (tid)
  - `mid` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
