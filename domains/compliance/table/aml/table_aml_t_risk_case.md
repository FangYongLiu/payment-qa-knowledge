---
id: tbl_aml_t_risk_case
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
- t_risk_case
subdomain: aml
module: null
sensitivity: normal
name: 风险案件信息(t_risk_case)
aliases:
- t_risk_case
related_services:
- svc_aml
related_scenarios: []
---
# 风险案件信息(t_risk_case)

## 用途
风险案件信息。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `transaction_id` | varchar(64) |  | 交易ID |
| `payment_order_no` | varchar(64) |  | 支付订单号 |
| `member_id` | varchar(32) |  | 会员id |
| `pay_amount` | decimal(15,4) |  | 支付金额 |
| `charge_back_amount` | decimal(15,4) |  | 拒付金额 |
| `indemnity_amount` | decimal(15,4) |  | 赔付金额 |
| `currency` | varchar(20) |  | 币种 |
| `case_type` | varchar(128) |  | case_type |
| `case_category` | varchar(32) |  | case category |
| `status` | varchar(10) |  | 案件状态 |
| `charge_back_status` | varchar(50) |  | 拒付处理状态 |
| `control_status` | varchar(20) |  | 控制状态 |
| `black_list` | varchar(255) |  | 黑名单 |
| `memo` | varchar(255) |  | 备注 |
| `operator` | varchar(20) |  | 操作人 |
| `refund_order_no` | varchar(20) |  | 退款订单号 |
| `recover_order_no` | varchar(20) |  | 追回资金订单号 |
| `biz_product_code` | varchar(10) |  | 业务产品码 |
| `card_no` | varchar(30) |  | 银行卡号 |
| `card_first_six` | char(6) |  | 银行卡号前六 |
| `card_last_four` | char(4) |  | 银行卡号后四 |
| `pay_channel` | char(4) |  | 支付方式 |
| `payee_id` | varchar(20) |  | 收款人id |
| `merchant_id` | varchar(20) |  | 商户id |
| `extension` | varchar(255) |  | 扩展字段 |
| `inst_order_no` | varchar(30) |  | 机构订单号 |
| `auth_id` | varchar(32) |  | ID |
| `version` | int | 默认 1 | 版本 |
| `mail_flag` | tinyint | 默认 0 | mail flag |
| `cash_flows` | varchar(200) |  | cash flows |
| `in_charge` | varchar(32) |  | in charge |
| `fund_channel` | varchar(32) |  | fund Channel |
| `reason_code` | varchar(50) |  | reason_code |
| `arn` | varchar(32) |  | arn |
| `case_source` | varchar(64) |  | case_source |
| `label` | varchar(128) |  | label |
| `create_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_payment_order_no` 唯一 (payment_order_no)
- 索引:
  - `idx_case_create_time` (create_time)
  - `idx_case_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
