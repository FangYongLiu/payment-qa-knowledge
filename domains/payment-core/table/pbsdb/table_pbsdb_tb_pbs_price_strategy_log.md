---
id: tbl_pbsdb_tb_pbs_price_strategy_log
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_pbs_price_strategy_log
subdomain: pricing
module: null
sensitivity: normal
name: 算费计算日志表(tb_pbs_price_strategy_log)
aliases:
- tb_pbs_price_strategy_log
related_services:
- svc_pbs
related_scenarios: []
---
# 算费计算日志表(tb_pbs_price_strategy_log)

## 用途
算费计算日志表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `request_no` | varchar(64) | NOT NULL | 请求号 |
| `party_id` | varchar(20) |  | 参与方id |
| `party_role` | varchar(12) | NOT NULL | 参与方角色 |
| `partner_id` | varchar(20) |  | 平台方 |
| `sec_merchant_id` | varchar(32) |  | 二级商户号 |
| `pay_channel` | varchar(6) | NOT NULL | 支付渠道 |
| `payment_code` | varchar(6) |  | 支付编码 |
| `product_code` | varchar(10) | NOT NULL | 产品码 |
| `order_amount` | decimal(15,4) | NOT NULL | 支付金额 |
| `price_strategy_id` | bigint | NOT NULL | 策略id |
| `price_strategy_param_id` | bigint | NOT NULL | 策略扩展id |
| `price_cal_id` | bigint | NOT NULL | 价格策略id |
| `price_cal_range_id` | bigint |  | 价格策略区间id |
| `fee_amount` | decimal(15,4) | NOT NULL | 费用金额 |
| `currency` | varchar(3) | NOT NULL | 币种 |
| `trade_type` | varchar(12) | NOT NULL | 交易：trade；退款：refund |
| `recipient_fee` | decimal(15,4) |  | recipient fee |
| `vat` | decimal(15,4) |  | vat |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modified` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
