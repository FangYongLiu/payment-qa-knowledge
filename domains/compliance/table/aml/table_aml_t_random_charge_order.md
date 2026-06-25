---
id: tbl_aml_t_random_charge_order
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
- t_random_charge_order
subdomain: aml
module: null
sensitivity: normal
name: random charge订单表(t_random_charge_order)
aliases:
- t_random_charge_order
related_services:
- svc_aml
related_scenarios: []
---
# random charge订单表(t_random_charge_order)

## 用途
random charge订单表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `trade_request_no` | bigint | PK / NOT NULL | 交易请求号 |
| `transaction_id` | bigint |  | 交易订单号 |
| `relative_payment_order` | bigint | NOT NULL | 关联的支付订单(对应的大额交易订单) |
| `payer_id` | varchar(20) | NOT NULL | 付款方ID |
| `payee_id` | varchar(20) | NOT NULL | 收款方ID |
| `amount` | decimal(19,4) | NOT NULL | 交易金额 |
| `currency` | char(3) | NOT NULL | 交易币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `card_id` | varchar(20) | NOT NULL | 卡id |
| `card_no` | varchar(20) | NOT NULL | 卡号 |
| `trade_status` | varchar(10) | NOT NULL | 交易状态：W=等待付款，C=关闭，PS=付款成功，F=付款失败，RW=退款等待，RS=退款成功 |
| `ticket` | varchar(32) | NOT NULL | 核身ticket |
| `extension` | varchar(255) |  | 扩展参数 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `pay_success_time` | timestamp |  | 付款成功时间 |
| `expire_time` | timestamp |  | 过期时间 |
| `refund_time` | timestamp |  | 退款发起时间 |
| `refund_finish_time` | timestamp |  | 退款完成时间 |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`trade_request_no`)
- 索引:
  - `idx_expire_time` (expire_time)
  - `idx_random_charge_ticket` (ticket)
  - `idx_update_time_payer_id` (update_time, payer_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
