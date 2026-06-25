---
id: tbl_trade_t_pay_method
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
- t_pay_method
subdomain: trade
module: null
sensitivity: normal
name: 支付方式(t_pay_method)
aliases:
- t_pay_method
related_services:
- svc_tradeii
related_scenarios: []
---
# 支付方式(t_pay_method)

## 用途
支付方式。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PAY_METHOD_ID` | decimal(17) | PK / NOT NULL | 支付渠道ID |
| `PAYMENT_VOUCHER_NO` | varchar(32) | NOT NULL | 支付凭证号 |
| `AMOUNT` | decimal(15,4) | NOT NULL | 金额 |
| `PAY_MODE` | varchar(32) | NOT NULL | 支付模式 |
| `PAY_CHANNEL` | varchar(32) | NOT NULL | 支付渠道 |
| `PROPS` | varchar(1000) |  | 渠道属性 |
| `EXTENSION` | varchar(4000) |  | 扩展参数 |
| `INST_PAY_NO` | varchar(32) |  | 提交机构订单号 |
| `RESULT_EXT` | varchar(1000) |  | 渠道结果扩展参数 |
| `GMT_PAY` | timestamp |  | 支付完成时间 |
| `UNIT_RESULT_CODE` | varchar(50) |  | 结果代码 |
| `UNIT_RESULT_MSG` | varchar(256) |  | 统一返回信息 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`PAY_METHOD_ID`)
- 索引:
  - `IDX_PAY_METHOD_I_P_NO` (INST_PAY_NO)
  - `IDX_PM_PAYMENT_VN` (PAYMENT_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
