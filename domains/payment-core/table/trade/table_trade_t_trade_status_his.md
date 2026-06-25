---
id: tbl_trade_t_trade_status_his
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
- t_trade_status_his
subdomain: trade
module: null
sensitivity: normal
name: 交易状态历史(t_trade_status_his)
aliases:
- t_trade_status_his
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易状态历史(t_trade_status_his)

## 用途
交易状态历史。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `HIS_ID` | decimal(11) | PK / NOT NULL | 交易状态历史ID |
| `TRADE_VOUCHER_NO` | varchar(32) | NOT NULL | 交易凭证号 |
| `PRE_STATUS` | varchar(16) |  | 前一状态 |
| `STATUS` | varchar(16) |  | 当前状态 |
| `MEMO` | varchar(128) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`HIS_ID`)
- 索引:
  - `IDX_TSH_GMT_MODIFIED` (GMT_MODIFIED)
  - `IDX_TSH_TRADE_VN` (TRADE_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
