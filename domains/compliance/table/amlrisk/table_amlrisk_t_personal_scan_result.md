---
id: tbl_amlrisk_t_personal_scan_result
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
- t_personal_scan_result
subdomain: amlrisk
module: null
sensitivity: normal
name: 个人会员扫描结果(t_personal_scan_result)
aliases:
- t_personal_scan_result
related_services:
- svc_aml
related_scenarios: []
---
# 个人会员扫描结果(t_personal_scan_result)

## 用途
个人会员扫描结果。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `personal_id` | bigint |  | 个人信息id |
| `member_id` | varchar(20) | NOT NULL | ID |
| `query_uid` | varchar(36) | NOT NULL | focal查询uuid |
| `screen_result` | varchar(2000) |  | 扫描结果（json） |
| `risk_assessment` | varchar(2000) |  | 评级结果（json） |
| `CREATED_TIME` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_mid` (query_uid)
  - `idx_pid` (personal_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
