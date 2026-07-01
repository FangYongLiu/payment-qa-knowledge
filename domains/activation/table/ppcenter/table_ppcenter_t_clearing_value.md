---
id: tbl_ppcenter_t_clearing_value
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_clearing_value
subdomain: pricing
module: null
sensitivity: normal
name: 清结算配置值(t_clearing_value)
aliases:
- t_clearing_value
related_services:
- svc_ppcenter
related_scenarios: []
---
# 清结算配置值(t_clearing_value)

## 用途
清结算配置值。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(12) | PK / AUTO_INC | 主键 |
| `pay_channel` | varchar(12) |  | 支付渠道 |
| `priority` | int(6) |  | 优先级(优先级的数字越大，优先级越高) |
| `deal_type` | varchar(16) |  | 11:即时到账收单交易;14退款;15:合并支付;16:交易;17:预授权交易 |
| `settlement_cycle` | int |  | 结算周期，单位是分钟 |
| `settlement_type` | char | NOT NULL | 结算类型：R-实时；T-时间触发；O：外部触发； |
| `execute_expression` | varchar(255) |  | 表达式 |
| `cron_define` | varchar(255) |  | 结算周期corn表达式 |
| `gmt_effective` | timestamp |  | 生效时间 |
| `gmt_invalid` | timestamp |  | 失效时间 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
