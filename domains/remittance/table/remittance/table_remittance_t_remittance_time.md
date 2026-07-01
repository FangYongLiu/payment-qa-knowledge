---
id: tbl_remittance_t_remittance_time
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
- t_remittance_time
subdomain: remittance
module: null
sensitivity: normal
name: 汇款时效(t_remittance_time)
aliases:
- t_remittance_time
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款时效(t_remittance_time)

## 用途
汇款时效。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `channel_code` | varchar(12) | NOT NULL | 渠道号 |
| `country_code` | varchar(7) | NOT NULL | 国家Code;2位国家码 |
| `transaction_mode` | varchar(20) | NOT NULL | 汇款方式;bank_transfer,cash_pick_up |
| `source_currency` | char(7) | NOT NULL | 原币种 |
| `target_currency` | char(7) | NOT NULL | 目标币种;收款的币种 |
| `delivery_time` | varchar(6) | NOT NULL | 到账时效;R:实时，D+0,D+0,T+0,T+1 |
| `time_desc` | varchar(100) | NOT NULL | 时效描述 |
| `speed_time` | int(8) | NOT NULL | 到账时间 |
| `channel_delivery_time` | varchar(255) |  | 渠道到账时效;渠道对到账时效的描述 |
| `channel_service_period` | varchar(100) |  | 渠道服务描述 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
