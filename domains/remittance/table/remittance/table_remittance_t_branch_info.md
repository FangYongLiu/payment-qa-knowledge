---
id: tbl_remittance_t_branch_info
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_branch_info
subdomain: remittance
module: null
sensitivity: normal
name: 分支行信息(t_branch_info)
aliases:
- t_branch_info
related_services:
- svc_remittance
related_scenarios: []
---
# 分支行信息(t_branch_info)

## 用途
分支行信息。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `bank_code` | varchar(16) | NOT NULL | 银行code |
| `country_code` | varchar(12) | NOT NULL | 国家code |
| `branch_code` | varchar(32) | NOT NULL | 分支code |
| `branch_name` | varchar(255) |  | 分支行名称 |
| `area` | varchar(255) |  | 地区 |
| `city` | varchar(255) |  | 城市 |
| `address` | varchar(255) |  | 具体地址 |
| `swift_code` | varchar(16) |  | SwiftCode |
| `routing_code` | varchar(12) |  | routing_code |
| `default_flag` | char |  | 默认标识 |
| `enable_flag` | char | NOT NULL | Y：可用，N：不可用 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_bank_branch` (bank_code, branch_name)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
