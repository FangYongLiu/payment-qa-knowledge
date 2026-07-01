---
id: tbl_remittance_t_out_market_rate
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
- t_out_market_rate
subdomain: remittance
module: null
sensitivity: normal
name: 外部市场汇率(t_out_market_rate)
aliases:
- t_out_market_rate
related_services:
- svc_remittance
related_scenarios: []
---
# 外部市场汇率(t_out_market_rate)

## 用途
外部市场汇率。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键ID |
| `source` | varchar(20) | NOT NULL | 汇率来源 |
| `source_currency` | char(3) | NOT NULL | 原币种 |
| `target_currency` | char(3) | NOT NULL | 目标币种 |
| `target_country_alpha3` | char(3) | NOT NULL | 3位国家CODE |
| `target_country` | char(2) | NOT NULL | 2位国家CODE |
| `transaction_mode` | varchar(15) | NOT NULL | 汇款模式 |
| `exchange_rate` | decimal(15,8) | NOT NULL | 汇率 |
| `version` | bigint | NOT NULL | 版本号（时间戳） |
| `rate_date` | datetime | NOT NULL | 汇率日期（不带时间） |
| `status` | char | NOT NULL | 是否有效 Y:有效,N:无效 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
