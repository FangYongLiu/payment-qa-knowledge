---
id: tbl_amlrisk_t_personal_scan_info
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
- t_personal_scan_info
subdomain: amlrisk
module: null
sensitivity: normal
name: 个人信息表(t_personal_scan_info)
aliases:
- t_personal_scan_info
related_services:
- svc_aml
related_scenarios: []
---
# 个人信息表(t_personal_scan_info)

## 用途
个人信息表。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `eid` | varchar(20) |  | eid |
| `full_name` | varchar(100) |  | 会员姓名 |
| `first_name` | varchar(100) |  | first name |
| `middle_name` | varchar(100) |  | middle name |
| `last_name` | varchar(100) |  | last name |
| `birthdate` | date |  | 出生日期 |
| `nationality` | varchar(10) |  | 国籍 |
| `gender` | char |  | 性别 |
| `country_of_birth` | varchar(10) |  | 出生国家 |
| `id_expiry_date` | date |  | eid过期日期 |
| `mobile` | varchar(20) |  | 手机号 |
| `marital_status` | char |  | 婚姻状态 |
| `employer_name` | varchar(100) |  | 雇主名称 |
| `industry` | varchar(100) |  | 所属行业 |
| `profession` | varchar(50) |  | 职业 |
| `query_uid` | varchar(80) |  | focal返回的queryuid |
| `decision` | varchar(20) |  | approve | reject | ignore | pending | reject and report |
| `query_status` | varchar(10) |  | FINISHED/WAITING_RESULTS/ON_GOING_SEARCH |
| `total_risk_score` | int |  | riskscore |
| `risk_result` | varchar(10) |  | High/Medium/Low |
| `match_number` | int |  | 匹配的数量 |
| `approve_status` | varchar(32) |  | 审核状态 |
| `ref_member_ids` | varchar(64) |  | 关联mids |
| `latest_result_id` | bigint |  | 最近一次返回结果ID |
| `extend` | varchar(500) |  | 扩展字段 |
| `result_extend` | varchar(500) |  | Save the results of external processing |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_personal_eid` (eid)
  - `idx_personal_updated_time` (updated_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
