---
id: tbl_pbsdb_tb_pbs_bill
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
- tb_pbs_bill
subdomain: pricing
module: null
sensitivity: normal
name: 计费账单(tb_pbs_bill)
aliases:
- tb_pbs_bill
related_services:
- svc_pbs
related_scenarios: []
---
# 计费账单(tb_pbs_bill)

## 用途
计费账单。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BILL_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `BIZ_NO` | varchar(32) | NOT NULL | 主键ID |
| `POSTING_CODE` | varchar(32) | NOT NULL | 业务子代码 |
| `ACCOUNT_DATE` | varchar(8) | NOT NULL | 账务时间 |
| `PRICE_STRATEGY_DETAIL_ID` | decimal(15) |  | 定价策略明细ID |
| `STATUS` | varchar(2) | NOT NULL | 账单状态 C-初始创建 P-支付完成 F-支付失败 |
| `TYPE` | decimal(2) | NOT NULL | 账单种类 0 - 实时账单 1 - 后计费账单 |
| `MEMO` | varchar(100) |  | 备注 |
| `BILL_FIN_TIME` | timestamp |  | 计费完成时间 |
| `FEE_AMOUNT` | decimal(15,4) | NOT NULL | 费用金额 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建日期 |

## 主键 / 索引
- 主键:(`BILL_ID`)
- 唯一约束:
  - `U_PBS_BILL_BIZNO` 唯一 (BIZ_NO)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
