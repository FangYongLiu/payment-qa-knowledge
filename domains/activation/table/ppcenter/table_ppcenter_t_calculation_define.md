---
id: tbl_ppcenter_t_calculation_define
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
- t_calculation_define
subdomain: pricing
module: null
sensitivity: normal
name: 费率定义(t_calculation_define)
aliases:
- t_calculation_define
related_services:
- svc_ppcenter
related_scenarios: []
---
# 费率定义(t_calculation_define)

## 用途
费率定义。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `name` | varchar(128) | NOT NULL | 费率配置名称 |
| `product_template_id` | int |  | 模板id |
| `strategy_type` | int | NOT NULL | 策略类型 1.定额 2.阶梯定额 3.费率 4.阶梯费率 5按比例退费 7.合同期累计阶梯费率 8.合同期累计交易次数阶梯 9合同期累计交易流量阶梯 |
| `party_role` | varchar(12) | NOT NULL | 角色 |
| `pay_channel` | varchar(12) |  | 支付渠道 |
| `currency` | varchar(6) |  | 币种,如AED |
| `scenes` | varchar(12) |  | 场景 |
| `payment_code` | varchar(12) |  | 支付编码 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `effective_duration` | varchar(16) |  | 算费模板生效时长 |
| `period` | tinyint(2) |  | 算费分段 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
