---
id: tbl_pbsdb_tb_pbs_price_cal_range
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
- tb_pbs_price_cal_range
subdomain: pricing
module: null
sensitivity: normal
name: 计价区间(tb_pbs_price_cal_range)
aliases:
- tb_pbs_price_cal_range
related_services:
- svc_pbs
related_scenarios: []
---
# 计价区间(tb_pbs_price_cal_range)

## 用途
计价区间。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `RANGE_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `PRICE_CAL_ID` | decimal(15) | NOT NULL | 价格计算策略ID |
| `RANGE_FROM` | decimal(15,4) |  | 区间上限 |
| `RANGE_FROM_INCLUDE` | decimal(1) |  | 区间上限包含标志 1-包含 0-不包含 |
| `RANGE_TO` | decimal(15,4) |  | 区间下限 |
| `STATUS` | char | NOT NULL | 状态 C-创建 A-可用 D-废弃 |
| `FIX_CHARGE` | decimal(15,4) |  | 费额 |
| `RATE` | decimal(15,4) |  | 费率 |
| `RANGE_TO_INCLUDE` | decimal(1) |  | 区间下限包含标志 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`RANGE_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
