---
id: tbl_aml_t_risk_refund_mail
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
- t_risk_refund_mail
subdomain: aml
module: null
sensitivity: normal
name: 拒付邮件信息表(t_risk_refund_mail)
aliases:
- t_risk_refund_mail
related_services:
- svc_aml
related_scenarios: []
---
# 拒付邮件信息表(t_risk_refund_mail)

## 用途
拒付邮件信息表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `mail_digest` | varchar(32) |  | mail digest |
| `subject` | varchar(64) |  | subject |
| `rc` | varchar(64) |  | 邮件标题 |
| `credit_card` | varchar(32) |  | 银行卡号 |
| `merchant_id` | varchar(16) |  | 商户ID |
| `trade_date` | varchar(16) |  | 交易时间 |
| `trade_date_time` | timestamp |  | 交易日期 |
| `trade_amount` | varchar(16) |  | 交易金额 |
| `trade_amount_num` | decimal(12,4) |  | 交易金额 |
| `auth_id` | varchar(16) |  | 授权ID |
| `arn` | varchar(32) |  | arn |
| `case_pool_flag` | tinyint |  | 是否添加案例库 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建日期 |
| `payment_order_no` | varchar(20) |  | 支付订单号 |
| `inst_order_no` | varchar(20) |  | 机构订单号 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
