---
id: tbl_trade_t_market_method
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (trade schema) 2026-06-25
tags:
- trade
- trade
- t_market_method
subdomain: trade
module: null
sensitivity: normal
name: 营销服务表(t_market_method)
aliases:
- t_market_method
related_services:
- svc_tradeii
related_scenarios: []
---
# 营销服务表(t_market_method)

## 用途
营销服务表。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `trade_voucher_no` | varchar(32) | NOT NULL | 交易凭证号 |
| `party_role` | varchar(32) | NOT NULL | 抵扣角色 DEDUCT |
| `account_no` | varchar(32) |  | 抵扣账户 |
| `market_type` | varchar(10) | NOT NULL | 抵扣方式：GP、COUPON、CUT立减 |
| `amount` | decimal(15,4) | NOT NULL | 抵扣金额 |
| `gp_amount` | decimal(15,4) |  | 抵扣数量（GP才有） |
| `exchange_rate` | int |  | 兑换汇率 |
| `currency` | char(3) | NOT NULL | 币种 |
| `market_voucher_no` | varchar(64) |  | 业务ID |
| `status` | varchar(20) | NOT NULL | 支付状态：I(初始处理中) FP(冻结中) FS(已冻结)、CP(撤销中) CS(撤销成功) SS(结算成功) FF(冻结失败) RP(退款中) RF(退款失败)  RS(退还成功) |
| `error_code` | varchar(50) |  | 失败码 |
| `error_message` | varchar(125) |  | 失败原因 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modified` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_gmt_modified` (gmt_modified)
  - `idx_trade_voucher_no` (trade_voucher_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
