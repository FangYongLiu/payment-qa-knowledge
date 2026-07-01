---
id: tbl_amlrisk_t_personal_ref
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
- t_personal_ref
subdomain: amlrisk
module: null
sensitivity: normal
name: 个人信息关联表(t_personal_ref)
aliases:
- t_personal_ref
related_services:
- svc_aml
related_scenarios: []
---
# 个人信息关联表(t_personal_ref)

## 用途
个人信息关联表。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `personal_id` | bigint |  | 个人信息表id |
| `member_id` | varchar(20) |  | 会员id |
| `mobile` | varchar(20) |  | 手机号 |
| `screen_type` | varchar(16) |  | screen type |
| `CREATED_TIME` | timestamp |  | 创建时间 |
| `UPDATED_TIME` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_mid` (member_id)
  - `idx_pid` (personal_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
