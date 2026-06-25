---
id: tbl_amlrisk_t_freeze_member
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
- t_freeze_member
subdomain: amlrisk
module: null
sensitivity: normal
name: 冻结用户(t_freeze_member)
aliases:
- t_freeze_member
related_services:
- svc_aml
related_scenarios: []
---
# 冻结用户(t_freeze_member)

## 用途
冻结用户。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) |  | 会员id |
| `target_status` | varchar(10) |  | 目标状态（freeze/stop_out/stop_in） |
| `finish_flag` | char |  | 完成标志(y/n) |
| `finish_time` | timestamp |  | 完成时间 |
| `reason` | varchar(200) |  | 原因 |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_mid` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
