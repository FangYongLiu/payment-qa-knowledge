---
id: tbl_pbsdb_tb_pbs_bill_workorder
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
- tb_pbs_bill_workorder
subdomain: pricing
module: null
sensitivity: normal
name: 计费工单表(tb_pbs_bill_workorder)
aliases:
- tb_pbs_bill_workorder
related_services:
- svc_pbs
related_scenarios: []
---
# 计费工单表(tb_pbs_bill_workorder)

## 用途
计费工单表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BILL_WORORDER_ID` | decimal(15) | PK / NOT NULL | 账单组 |
| `BILL_WORORDER_BATCHNO` | decimal(15) |  | 账单批次 |
| `REQUEST_ID` | varchar(32) |  | 主键ID |
| `BILL_ID` | decimal(15) |  | 账单ID |
| `STATUS` | varchar(2) | NOT NULL | 工单状态 C-创建 AA-审核申请中 AF-申请被拒绝 AS-申请通过 S-操作完成 F-操作失败 |
| `TYPE` | varchar(5) | NOT NULL | P-算费 BC-生成账单 BP-支付账单 BCP-生成并支付账单 BS-同步账单状态 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修订人 |
| `CREATE_BY` | varchar(50) |  | 创建者 |

## 主键 / 索引
- 主键:(`BILL_WORORDER_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
