---
id: tbl_remittance_t_proper_charge_strategy
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
- t_proper_charge_strategy
subdomain: remittance
module: null
sensitivity: normal
name: 专有计费策略(t_proper_charge_strategy)
aliases:
- t_proper_charge_strategy
related_services:
- svc_remittance
related_scenarios: []
---
# 专有计费策略(t_proper_charge_strategy)

## 用途
专有计费策略。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `strategy_id` | int | PK / AUTO_INC | 主键 |
| `name_key` | varchar(25) | NOT NULL | 关键词 |
| `channel_code` | varchar(10) | NOT NULL | 渠道code |
| `transaction_mode` | varchar(16) | NOT NULL | 汇款模式 |
| `fix_charge` | decimal(15,4) |  | 固定费用 |
| `fix_rate` | decimal(15,8) |  | 固定费率 |
| `effect_time` | datetime |  | 生效时间 |
| `expired_time` | datetime |  | 过期时间 |
| `operator_name` | varchar(100) |  | 操作员名称 |
| `version` | int(5) | 默认 0 | 版本号 |
| `status` | char(2) | NOT NULL | 状态 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`strategy_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
