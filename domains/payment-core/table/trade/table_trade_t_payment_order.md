---
id: tbl_trade_t_payment_order
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
- t_payment_order
subdomain: trade
module: null
sensitivity: normal
name: 支付订单(t_payment_order)
aliases:
- t_payment_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 支付订单(t_payment_order)

## 用途
支付订单。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PAYMENT_VOUCHER_NO` | varchar(32) | PK / NOT NULL | 支付凭证号 |
| `PAYMENT_SOURCE_VOUCHER_NO` | varchar(64) |  | 支付原始凭证号 |
| `ORIG_PAYMENT_VOUCHER_NO` | varchar(32) |  | 原支付凭证号 |
| `BIZ_PRODUCT_CODE` | varchar(16) | NOT NULL | 业务产品编码 |
| `IS_DUPLICATE` | char |  | 是否重复支付 |
| `PAYMENT_TYPE` | varchar(16) | NOT NULL | 支付类型 |
| `PAYMENT_CODE` | varchar(16) |  | 支付编码 |
| `AMOUNT` | decimal(15,4) | NOT NULL | 支付金额 |
| `STATUS` | varchar(16) | NOT NULL | 支付状态 |
| `pay_scene` | varchar(32) |  | 支付场景 |
| `GMT_SUBMIT` | timestamp |  | 支付提交时间 |
| `ACCESS_CHANNEL` | varchar(16) |  | 终端类型 |
| `ERROR_CODE` | varchar(128) |  | 错误编码 |
| `ERROR_MSG` | varchar(256) |  | 错误信息 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `PAYMENT_TAG` | varchar(16) |  | 支付标签相对于支付类型来说比较自由，可以认为是支付类型下的子分类 INST_SETTLE:即时结算 |
| `TRADE_VOUCHER_NO` | varchar(32) |  | 交易凭证号 |
| `PROCESSOR_ID` | varchar(64) |  | 处理器ID |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `MEMO` | varchar(256) |  | 备注 |
| `RETRY_FLAG` | varchar(1) |  | 重试标记 Y:重试中 N：非重试中 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`PAYMENT_VOUCHER_NO`)
- 索引:
  - `IDX_PO_ORIG_PAYMENT_VN` (ORIG_PAYMENT_VOUCHER_NO)
  - `IDX_PO_TRADE_VN` (TRADE_VOUCHER_NO)
  - `IDX_TO_GMT_MODIFIED` (GMT_MODIFIED)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
