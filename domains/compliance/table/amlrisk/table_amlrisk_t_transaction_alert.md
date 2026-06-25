---
id: tbl_amlrisk_t_transaction_alert
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_transaction_alert
subdomain: amlrisk
module: null
sensitivity: normal
name: 交易监控alert(t_transaction_alert)
aliases:
- t_transaction_alert
related_services:
- svc_aml
related_scenarios: []
---
# 交易监控alert(t_transaction_alert)

## 用途
交易监控alert。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `alert_uid` | varchar(64) | NOT NULL | alert_uid |
| `transaction_id` | varchar(32) |  | 交易id |
| `rule_name` | varchar(200) |  | alert的规则名称 |
| `status` | varchar(10) |  | 状态 WAIT_CHECK/FINISH |
| `CREATED_TIME` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_alert_uid` 唯一 (alert_uid)
- 索引:
  - `idx_transaction_id` (transaction_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
