---
id: tbl_aml_t_refund_order
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
- t_refund_order
subdomain: aml
module: null
sensitivity: normal
name: 退款表(t_refund_order)
aliases:
- t_refund_order
related_services:
- svc_aml
related_scenarios: []
---
# 退款表(t_refund_order)

## 用途
退款表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `refund_request_no` | bigint | PK / NOT NULL | 退款请求号 |
| `orig_transaction_id` | varchar(20) | NOT NULL | 原交易请求号 |
| `orig_payment_order_no` | varchar(32) | NOT NULL | 原支付订单号 |
| `refund_amount` | decimal(19,4) | NOT NULL | 退款金额 |
| `currency` | char(3) | NOT NULL | 交易币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `refund_status` | varchar(10) | NOT NULL | 退款状态：P=处理中，S=成功，F=失败 |
| `extension` | varchar(255) |  | 扩展参数 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `finish_time` | timestamp |  | 结束时间 |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`refund_request_no`)
- 索引:
  - `idx_payment_order_no` (orig_payment_order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
