---
id: tbl_aml_t_entry_account
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
- t_entry_account
subdomain: aml
module: null
sensitivity: normal
name: 登账表(t_entry_account)
aliases:
- t_entry_account
related_services:
- svc_aml
related_scenarios: []
---
# 登账表(t_entry_account)

## 用途
登账表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `payment_order_no` | bigint | PK / NOT NULL | 支付订单号 |
| `payer_id` | varchar(20) | NOT NULL | 付款方ID |
| `payer_account_no` | varchar(32) | NOT NULL | 付款方账户号 |
| `payee_id` | varchar(20) | NOT NULL | 收款方ID |
| `payee_account_no` | varchar(32) | NOT NULL | 收款方账户号 |
| `amount` | decimal(19,4) | NOT NULL | 交易金额 |
| `currency` | char(3) | NOT NULL | 交易币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `trade_status` | varchar(10) | NOT NULL | 交易状态：PS=成功 F-失败 |
| `relative_payment_order` | varchar(64) | NOT NULL | 关联的支付订单(拒付的那笔) |
| `extension` | varchar(255) |  | 扩展参数 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `pay_success_time` | timestamp |  | 付款成功时间 |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`payment_order_no`)
- 索引:
  - `idx_relative_payment_order` (relative_payment_order)
  - `idx_update_time_payer_id` (update_time, payer_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
