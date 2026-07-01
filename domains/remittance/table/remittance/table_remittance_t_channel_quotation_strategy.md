---
id: tbl_remittance_t_channel_quotation_strategy
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
- t_channel_quotation_strategy
subdomain: remittance
module: null
sensitivity: normal
name: 计费策略(t_channel_quotation_strategy)
aliases:
- t_channel_quotation_strategy
related_services:
- svc_remittance
related_scenarios: []
---
# 计费策略(t_channel_quotation_strategy)

## 用途
计费策略。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `strategy_id` | int | PK / AUTO_INC | 主键 |
| `channel_code` | varchar(10) | NOT NULL | 渠道code |
| `channel_type` | char(6) |  | 渠道类型，direct-直连渠道，自主定义汇率；common-通用渠道，渠道定义汇率，存量MG的汇率需要补充数据 |
| `transaction_mode` | varchar(16) | NOT NULL | 汇款模式 |
| `source_currency` | varchar(7) | NOT NULL | 原币种 |
| `target_currency` | varchar(7) | NOT NULL | 目标币种 |
| `target_country_code` | varchar(7) | NOT NULL | 目标国家（两位） |
| `target_country_alpha3` | char(3) |  | 目标国家（三位） |
| `bl_amount` | decimal(15,4) |  | 汇率基准金额 |
| `exchange_rate` | decimal(15,8) |  | 汇率 |
| `corridor_fee` | decimal(15,4) |  | 通道费用 |
| `corridor_fee_currency` | char(3) |  |  |
| `vat` | decimal(15,4) |  | 税 |
| `version` | int(5) | NOT NULL / 默认 0 | 版本号 |
| `status` | char(2) | NOT NULL | 状态 |
| `change_flag` | char |  | 费率是否变化标记, Y/N |
| `buy_rate` | decimal(19,4) |  | 购买汇率 |
| `operator_name` | varchar(64) |  | 操作员名称 |
| `operator_time` | timestamp |  | 操作时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`strategy_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
