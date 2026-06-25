---
id: tbl_pbsdb_tb_pbs_strategy_log
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
- tb_pbs_strategy_log
subdomain: pricing
module: null
sensitivity: normal
name: 策略使用日志(tb_pbs_strategy_log)
aliases:
- tb_pbs_strategy_log
related_services:
- svc_pbs
related_scenarios: []
---
# 策略使用日志(tb_pbs_strategy_log)

## 用途
策略使用日志。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `STRATEGY_USE_ID` | decimal(15) | PK / NOT NULL | id |
| `BILL_WORORDER_ID` | decimal(15) |  | 计费工单ID |
| `PRICE_STRATEGY_ID` | decimal(15) |  | 定价策略ID |
| `PRICE_STRATEGY_DETAIL_ID` | decimal(15) |  | 定价明细ID |
| `PRICE_CAL_ID` | decimal(15) |  | 价格计算策略ID |
| `RANGE_ID` | decimal(15) |  | 计价区间ID |
| `ASSIGN_ID` | decimal(15) |  | 分摊分润ID |
| `ASSIGN_DETAIL_ID` | decimal(15) |  | 分摊分润策略明细ID |
| `BILL_STRATEGY_ID` | decimal(15) |  | 账单策略ID |
| `GMT_CREATE` | timestamp |  | 日志记录时间 |

## 主键 / 索引
- 主键:(`STRATEGY_USE_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
