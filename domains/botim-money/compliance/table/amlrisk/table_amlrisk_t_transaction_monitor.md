---
id: tbl_amlrisk_t_transaction_monitor
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_transaction_monitor
subdomain: amlrisk
module: null
sensitivity: normal
name: 交易监控(t_transaction_monitor)
aliases:
- t_transaction_monitor
related_services:
- svc_aml
related_scenarios: []
---
# 交易监控(t_transaction_monitor)

## 用途
交易监控。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `transaction_id` | varchar(32) |  | 交易id |
| `payment_order_no` | varchar(32) |  | 支付订单号 |
| `biz_product_code` | varchar(10) |  | 业务产品码 |
| `pay_channel` | varchar(10) |  | 支付方式 |
| `member_id` | varchar(20) |  | 会员id |
| `payee_member_id` | varchar(20) |  | 收款人id |
| `amount` | decimal(19,4) |  | 交易金额 |
| `currency` | char(3) |  | 币种 |
| `report_category` | varchar(32) |  | 上报类型 |
| `trade_time` | timestamp |  | 交易时间 |
| `memo` | varchar(200) |  | 备注 |
| `extension` | varchar(500) |  | 扩展字段 |
| `report_status` | varchar(20) |  | report status |
| `check_status` | varchar(20) |  | check status |
| `alerts` | varchar(500) |  | alerts (json) |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_monitor_member_id` (member_id)
  - `idx_monitor_payment_order_no` (payment_order_no)
  - `idx_monitor_transaction_id` (transaction_id)
  - `idx_monitor_updated_time` (updated_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
