---
id: tbl_trade_t_control_order
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
- t_control_order
subdomain: trade
module: null
sensitivity: normal
name: 交易控制表(t_control_order)
aliases:
- t_control_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易控制表(t_control_order)

## 用途
交易控制表。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CONTROL_VOUCHER_NO` | varchar(32) | PK / NOT NULL | 控制凭证号 |
| `CONTROL_SOURCE_VOUCHER_NO` | varchar(64) | NOT NULL | 原始控制凭证号 |
| `CONTROL_TYPE` | varchar(16) |  | 控制订单类型 |
| `ACCOUNT_TYPE` | varchar(16) |  | 账户类型 |
| `ACCOUNT_NO` | varchar(64) |  | 账号 |
| `STATUS` | varchar(16) |  | 控制订单状态 |
| `SUMMARY` | varchar(256) |  | 摘要 |
| `EXTENSION` | varchar(2000) |  | 扩展字段 |
| `ERROR_CODE` | varchar(128) |  | 错误码 |
| `ERROR_MESSAGE` | varchar(256) |  | 错误描述 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `TRADE_VOUCHER_NO` | varchar(32) | NOT NULL | 交易凭证号 |
| `RELATED_CONTROL_VOUCHER_NO` | varchar(32) |  | 相关控制凭证号 |
| `RELATED_BATCH_VOUCHER_NO` | varchar(32) |  | 相关批次凭证号 |

## 主键 / 索引
- 主键:(`CONTROL_VOUCHER_NO`)
- 索引:
  - `IDX_CTRL_GMT_CREATE` (GMT_CREATE)
  - `IDX_CTRL_SRC_VN` (CONTROL_SOURCE_VOUCHER_NO)
  - `IDX_CTRL_TRADE_VN` (TRADE_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
