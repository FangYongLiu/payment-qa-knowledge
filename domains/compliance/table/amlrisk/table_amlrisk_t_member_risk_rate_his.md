---
id: tbl_amlrisk_t_member_risk_rate_his
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
- t_member_risk_rate_his
subdomain: amlrisk
module: null
sensitivity: normal
name: member risk rate history(t_member_risk_rate_his)
aliases:
- t_member_risk_rate_his
related_services:
- svc_aml
related_scenarios: []
---
# member risk rate history(t_member_risk_rate_his)

## 用途
member risk rate history。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `member_id` | varchar(20) | NOT NULL | member_id(person eid| merchant member_id) |
| `id_no` | varchar(20) |  | eid |
| `member_type` | varchar(20) | NOT NULL | member_type(PERSONAL/MERCHANT) |
| `risk_rate_score` | decimal(19,4) | NOT NULL | risk_rate_score |
| `risk_rating` | varchar(20) | NOT NULL | risk_rating |
| `risk_rate_date` | timestamp(3) | NOT NULL | risk_rate_date |
| `params` | varchar(1024) | NOT NULL | params |
| `checked` | char | NOT NULL | checked(Y/N) |
| `status` | char(2) |  | status |
| `scan_date` | timestamp |  | last LN scan date |
| `send_date` | int |  | send date |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
