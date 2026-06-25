---
id: tbl_ppcenter_t_clearing_define
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_clearing_define
subdomain: pricing
module: null
sensitivity: normal
name: 清结算定义(t_clearing_define)
aliases:
- t_clearing_define
related_services:
- svc_ppcenter
related_scenarios: []
---
# 清结算定义(t_clearing_define)

## 用途
清结算定义。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `product_template_id` | int |  | 模板id |
| `name` | varchar(124) |  | name |
| `session_define` | varchar(64) |  | 场次定义 |
| `deal_type` | varchar(16) |  | 11:即时到账收单交易;14退款;15:合并支付;16:交易;17:预授权交易 |
| `settlement_cycle` | int |  | 结算周期，单位是分钟 |
| `settlement_type` | char | NOT NULL | 结算类型：R-实时；T-时间触发；O：外部触发； |
| `product_code` | varchar(32) |  | 产品编码 |
| `execute_expression` | varchar(256) |  | 表达式 |
| `gather_type` | varchar(2) |  | 汇总类型：N-不汇总；G-汇总；O-轧差；B-批量 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `priority` | int(16) |  | 优先级(优先级的数字越大，优先级越高) |
| `cron_define` | varchar(255) |  | 结算周期corn表达式 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
