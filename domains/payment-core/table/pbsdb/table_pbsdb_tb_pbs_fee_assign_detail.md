---
id: tbl_pbsdb_tb_pbs_fee_assign_detail
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
- tb_pbs_fee_assign_detail
subdomain: pricing
module: null
sensitivity: normal
name: 分润分摊策略明细表(tb_pbs_fee_assign_detail)
aliases:
- tb_pbs_fee_assign_detail
related_services:
- svc_pbs
related_scenarios: []
---
# 分润分摊策略明细表(tb_pbs_fee_assign_detail)

## 用途
分润分摊策略明细表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ASSIGN_DETAIL_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `ASSIGN_ID` | decimal(15) | NOT NULL | 主键ID |
| `ASSIGN_CHARGE` | decimal(15,4) | NOT NULL | 费额 |
| `RATE_FLAG` | char | NOT NULL | 费率标志，用来区分是费额还是费率 Y-费率 N-费用 |
| `ASSIGN_RATE` | decimal(8,6) | NOT NULL | 费率 |
| `ASSIGN_POSTING_CODE` | varchar(100) | NOT NULL | 分摊分润业务子代码 |
| `ASSIGN_PT` | varchar(32) |  | 分摊分润方的PT ID |
| `ASSIGN_ACCOUNTID` | varchar(32) |  | 账户 |
| `STATUS` | char | NOT NULL | 状态 C-创建 A-可用 D-废弃 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`ASSIGN_DETAIL_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
