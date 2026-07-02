---
id: tbl_reconciliation_t_weekly_report_tracking
object_type: Table
name: Weekly Report Tracking (t_weekly_report_tracking)
aliases: [t_weekly_report_tracking, reconciliation.t_weekly_report_tracking]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Weekly Report Tracking (t_weekly_report_tracking)

## 用途
物理表 `reconciliation.t_weekly_report_tracking`,主键 `tracking_id`。Weekly Report Tracking。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `tracking_id` | bigint | Tracking ID：eight before and nine after |
| `tracking_name` | varchar(128) | Tracking Name |
| `tracking_type` | varchar(32) | Tracking Type |
| `report_id` | bigint | Report ID · 可空 |
| `identity_source` | varchar(32) | Identity Source · 可空 |
| `risk_level` | char(3) | Risk Level · 可空 |
| `root_cause` | varchar(64) | Root Cause · 可空 |
| `risk_flag` | char | Y:Edited N:Not Edited · 可空 |
| `comment` | varchar(512) | Comment · 可空 |
| `issues` | varchar(512) | Issues · 可空 |
| `person_in_charge` | varchar(32) | Person In Charge · 可空 |
| `clear_time` | timestamp | Clear Time · 可空 |
| `status` | char | Status |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`tracking_id`
- `idx_reportId`:report_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
