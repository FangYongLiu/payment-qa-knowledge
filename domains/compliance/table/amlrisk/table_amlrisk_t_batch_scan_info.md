---
id: tbl_amlrisk_t_batch_scan_info
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
- t_batch_scan_info
subdomain: amlrisk
module: null
sensitivity: normal
name: 批量扫码临时表(t_batch_scan_info)
aliases:
- t_batch_scan_info
related_services:
- svc_aml
related_scenarios: []
---
# 批量扫码临时表(t_batch_scan_info)

## 用途
批量扫码临时表。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) |  | 会员id |
| `member_type` | char |  | 会员类型：1-个人，2-企业 |
| `member_label` | char |  | 会员标签：I-不活跃，D-休眠，A-活跃 |
| `eid` | varchar(20) |  | eid |
| `full_name` | varchar(100) |  | 会员姓名 |
| `birthdate` | date |  | 出生日期 |
| `nationality` | varchar(10) |  | 国籍 |
| `gender` | char |  | 性别 |
| `country_of_birth` | varchar(10) |  | 出生国家 |
| `id_expiry_date` | date |  | eid过期日期 |
| `mobile` | varchar(20) |  | 手机号 |
| `marital_status` | varchar(10) |  | 婚姻状态 |
| `employer_name` | varchar(100) |  | 雇主名称 |
| `profession` | varchar(50) |  | 职业 |
| `merchant_name` | varchar(100) |  | 商户名称 |
| `industry` | varchar(100) |  | 所属行业 |
| `country_of_incorporation` | varchar(10) |  | 所在国家 |
| `onboarding_channel` | varchar(20) |  | 渠道 |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
