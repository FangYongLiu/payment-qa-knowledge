---
id: tbl_remittance_t_funding_record
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
- t_funding_record
subdomain: remittance
module: null
sensitivity: normal
name: funding record(t_funding_record)
aliases:
- t_funding_record
related_services:
- svc_remittance
related_scenarios: []
---
# funding record(t_funding_record)

## 用途
funding record。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `channel_code` | varchar(20) | NOT NULL | channel code |
| `country_code` | char(3) | NOT NULL | country code |
| `withdrawal_id` | varchar(32) |  | withdrawal id |
| `withdrawal_amount` | decimal(19,4) | NOT NULL | withdrawal amount |
| `fee` | decimal(19,4) |  | fee |
| `withdrawal_net_amount` | decimal(19,4) | NOT NULL | withdrawal net amount |
| `withdrawal_currency` | char(3) | NOT NULL | withdrawal currency |
| `exchange_rate` | varchar(15) | NOT NULL | exchange_rate |
| `received_amount` | decimal(19,4) | NOT NULL | received amount |
| `received_currency` | char(3) | NOT NULL | received currency |
| `status` | char | NOT NULL | status: V=Valid，C=Cancel |
| `funding_remark` | varchar(450) |  | funding remark |
| `funding_time` | timestamp | NOT NULL | funding date |
| `funding_operator` | varchar(100) | NOT NULL | funding operator |
| `cancel_remark` | varchar(450) |  | cancel remark |
| `cancel_time` | timestamp |  | cancel time |
| `cancel_operator` | varchar(100) |  | cancel operator |
| `extension` | varchar(255) |  | Extension |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
