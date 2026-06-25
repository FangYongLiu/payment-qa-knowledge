---
id: tbl_aml_t_charge_back_product_config
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_charge_back_product_config
subdomain: aml
module: null
sensitivity: normal
name: chargeback 产品配置表(t_charge_back_product_config)
aliases:
- t_charge_back_product_config
related_services:
- svc_aml
related_scenarios: []
---
# chargeback 产品配置表(t_charge_back_product_config)

## 用途
chargeback 产品配置表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_product_code` | char(10) | PK / NOT NULL | 业务产品码 |
| `funds_recover_source` | varchar(20) |  | 追回资金来源（PAYEE/PAYER/ASSIGN_ACCOUNT） |
| `recover_member_id` | varchar(20) |  | 追回资金指定会员 |
| `bill_notify` | varchar(20) |  | 账单通知（PERSONAL/MERCHANT） |
| `biz_refund_strategy` | varchar(20) |  | 业务退款策略 |
| `risk_refund_strategy` | varchar(20) |  | 风控退款策略 |
| `extension` | varchar(200) |  | extension |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`biz_product_code`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
