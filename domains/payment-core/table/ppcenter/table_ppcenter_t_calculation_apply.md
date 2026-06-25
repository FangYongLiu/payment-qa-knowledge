---
id: tbl_ppcenter_t_calculation_apply
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
- t_calculation_apply
subdomain: pricing
module: null
sensitivity: normal
name: 算费申请(t_calculation_apply)
aliases:
- t_calculation_apply
related_services:
- svc_ppcenter
related_scenarios: []
---
# 算费申请(t_calculation_apply)

## 用途
算费申请。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(12) | PK / AUTO_INC | 主键 |
| `party_id` | varchar(32) |  | 收费会员id |
| `party_role` | varchar(12) |  | 收费角色 |
| `strategy_type` | tinyint(2) | NOT NULL | 策略类型 1.定额 2.阶梯定额 3.费率 4.阶梯费率 5按比例退费 7.合同期累计阶梯费率 8.合同期累计交易次数阶梯 9合同期累计交易流量阶梯 |
| `pay_channel` | varchar(12) |  | 支付渠道 |
| `currency` | varchar(6) |  | 币种,如AED |
| `fix_rate` | decimal(8,6) | NOT NULL | 固定费率 |
| `fix_charge` | decimal(15,4) | NOT NULL | 固定费用 |
| `min_charge` | decimal(15,4) | NOT NULL | 费用下限 |
| `max_charge` | decimal(15,4) | NOT NULL | 费用上限 |
| `vat` | decimal(15,4) |  | vat |
| `cal_attr` | varchar(255) |  | 扩展参数 |
| `gmt_effective` | timestamp |  | 生效时间 |
| `gmt_invalid` | timestamp |  | 失效时间 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `apply_id` | int(12) |  | 申请id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
