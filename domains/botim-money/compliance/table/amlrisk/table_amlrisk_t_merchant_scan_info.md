---
id: tbl_amlrisk_t_merchant_scan_info
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
- t_merchant_scan_info
subdomain: amlrisk
module: null
sensitivity: normal
name: 商户扫描信息表(t_merchant_scan_info)
aliases:
- t_merchant_scan_info
related_services:
- svc_aml
related_scenarios: []
---
# 商户扫描信息表(t_merchant_scan_info)

## 用途
商户扫描信息表。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) |  | 会员id |
| `merchant_name` | varchar(100) |  | 商户名称 |
| `industry` | varchar(100) |  | 所属行业 |
| `country_of_incorporation` | varchar(10) |  | 所在国家 |
| `onboarding_channel` | varchar(20) |  | 渠道 |
| `length_of_relationship` | varchar(32) |  | length of relationship |
| `query_uid` | varchar(80) |  | focal返回的queryuid |
| `decision` | varchar(20) |  | approve | reject | ignore | pending | reject and report |
| `query_status` | varchar(10) |  | FINISHED/WAITING_RESULTS/ON_GOING_SEARCH |
| `total_risk_score` | int |  | riskscore |
| `risk_result` | varchar(10) |  | High/Medium/Low |
| `latest_result_id` | bigint |  | 最近一次返回结果ID |
| `CREATED_TIME` | timestamp |  | 创建时间 |
| `UPDATED_TIME` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
