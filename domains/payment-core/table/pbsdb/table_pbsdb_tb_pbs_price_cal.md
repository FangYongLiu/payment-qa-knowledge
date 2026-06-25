---
id: tbl_pbsdb_tb_pbs_price_cal
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
- tb_pbs_price_cal
subdomain: pricing
module: null
sensitivity: normal
name: 价格计算策略(tb_pbs_price_cal)
aliases:
- tb_pbs_price_cal
related_services:
- svc_pbs
related_scenarios: []
---
# 价格计算策略(tb_pbs_price_cal)

## 用途
价格计算策略。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PRICE_CAL_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `FIX_CHARGE` | decimal(15,4) | NOT NULL | 固定费用 |
| `FIX_RATE` | decimal(8,6) | NOT NULL | 固定费率 |
| `MAX_CHARGE` | decimal(15,4) | NOT NULL | 上限 |
| `MIN_CHARGE` | decimal(15,4) | NOT NULL | 下限 |
| `FORMULA_TYPE` | decimal(2) | NOT NULL | 计算公式类型 1-阶梯费率 2-阶梯费率累加 |
| `STATUS` | char | NOT NULL | C-创建 A-可用 D-废弃 |
| `MEMO` | varchar(300) |  | 描述 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`PRICE_CAL_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
