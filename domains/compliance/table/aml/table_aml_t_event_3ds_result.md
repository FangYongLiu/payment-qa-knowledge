---
id: tbl_aml_t_event_3ds_result
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
- t_event_3ds_result
subdomain: aml
module: null
sensitivity: normal
name: 渠道3ds认证表(t_event_3ds_result)
aliases:
- t_event_3ds_result
related_services:
- svc_aml
related_scenarios: []
---
# 渠道3ds认证表(t_event_3ds_result)

## 用途
渠道3ds认证表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL |  |
| `eci` | varchar(64) |  | eci |
| `ucaf` | varchar(64) |  | ucaf |
| `trade_order_no` | varchar(64) |  | 交易流水号 |
| `card_name` | varchar(64) |  | 持卡人姓名 |
| `bank_code` | varchar(64) |  | 银行编码-发卡行 |
| `bank_name` | varchar(64) |  | 银行名称-发卡行 |
| `card_no` | varchar(64) |  | ues卡号 |
| `card_prefix_rear` | varchar(64) |  | 卡前6****后4 |
| `card_brand` | varchar(64) |  | 卡品牌（卡组织） |
| `card_debit` | varchar(64) |  | 卡借贷标识 |
| `card_expire` | varchar(64) |  | 卡有效期 |
| `payment_order_no` | varchar(64) |  | 支付订单号 |
| `channel_order_no` | varchar(64) |  | 渠道订单号 |
| `channel_provide_no` | varchar(64) |  | 渠道编号,指3ds供应商的代码 |
| `identity_result` | varchar(64) |  | 认证结果--3ds |
| `identity_result_desc` | varchar(256) |  | 结果注释 |
| `request_channel_time` | varchar(64) |  | 上游请求渠道时间 |
| `request_time` | varchar(64) |  | 渠道请求银行的报文时间 |
| `response_time` | varchar(64) |  | 银行返回报文的时间 |
| `result_code_cvv2` | varchar(64) |  | cvv |
| `presence_Indicator_cvv2` | varchar(64) |  | cvv |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 系统时间 |
| `ext1` | varchar(64) |  | 扩展1 |
| `ext2` | varchar(64) |  | 扩展2 |
| `ext3` | varchar(64) |  | 扩展3 |
| `resultId` | varchar(64) |  | cmf落库主键 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx1_create_time` (create_time)
  - `idx1_trade_order_no` (trade_order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
