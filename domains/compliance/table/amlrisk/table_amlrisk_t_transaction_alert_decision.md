---
id: tbl_amlrisk_t_transaction_alert_decision
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
- t_transaction_alert_decision
subdomain: amlrisk
module: null
sensitivity: normal
name: 交易监控alert decision(t_transaction_alert_decision)
aliases:
- t_transaction_alert_decision
related_services:
- svc_aml
related_scenarios: []
---
# 交易监控alert decision(t_transaction_alert_decision)

## 用途
交易监控alert decision。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `decision_uid` | varchar(64) | NOT NULL | decision_uid |
| `alert_uid` | varchar(64) | NOT NULL | alert id |
| `transaction_id` | varchar(32) |  | 交易id |
| `decision` | varchar(20) |  | alert的决策 |
| `memo` | varchar(200) |  | 备注 |
| `CREATED_TIME` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_decision_uid` 唯一 (decision_uid)
- 索引:
  - `idx_alert_uid` (alert_uid)
  - `idx_transaction_id` (transaction_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
