---
id: tbl_pbsdb_tb_pbs_bill_detail
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
- tb_pbs_bill_detail
subdomain: pricing
module: null
sensitivity: normal
name: 计费账单明细表(tb_pbs_bill_detail)
aliases:
- tb_pbs_bill_detail
related_services:
- svc_pbs
related_scenarios: []
---
# 计费账单明细表(tb_pbs_bill_detail)

## 用途
计费账单明细表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BILL_DETAIL_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `BILL_ID` | decimal(15) | NOT NULL | 账单流水号 |
| `ASSIGN_DETAIL_ID` | decimal(15) |  | 分摊分润策略ID |
| `ASSIGN_AMOUNT` | decimal(15,4) | NOT NULL | 分摊分润金额 |
| `ASSIGN_POSTING_CODE` | varchar(32) | NOT NULL | 分摊分润业务代码 |
| `ASSIGN_FLAG` | varchar(2) | NOT NULL | 分润分摊标志 R-分润 T-分摊 G-共同 |
| `ASSIGN_PT` | varchar(64) |  | 无意义 |

## 主键 / 索引
- 主键:(`BILL_DETAIL_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
