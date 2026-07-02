---
id: tbl_remittance_t_beneficiary_address
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
- t_beneficiary_address
subdomain: remittance
module: null
sensitivity: normal
name: t_beneficiary_address
aliases:
- t_beneficiary_address
related_services:
- svc_remittance
related_scenarios: []
---
# t_beneficiary_address

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `beneficiary_info_id` | bigint | NOT NULL | 受益人id |
| `address_type` | varchar(12) | NOT NULL | 地址类型;PERMANENT,PRESENT |
| `is_default` | char |  | 是否默认地址；Y：是；N：否 |
| `country_code` | varchar(3) |  | 国家ISO code |
| `country_name` | varchar(255) |  | 国家名称 |
| `city` | varchar(100) |  | 城市 |
| `building` | varchar(255) |  | 建筑名称 |
| `street` | varchar(255) |  | 街道 |
| `area` | varchar(64) |  | 地区 |
| `province` | varchar(64) |  | 省份 |
| `room` | varchar(255) |  | 具体地址 |
| `post_code` | varchar(32) |  | 邮编 |
| `extension` | varchar(255) |  | 扩展信息 |
| `enable_flag` | char | NOT NULL | 启用标识: Y=启用，N=停用 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `t_beneficiary_bnf_ind` (beneficiary_info_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
