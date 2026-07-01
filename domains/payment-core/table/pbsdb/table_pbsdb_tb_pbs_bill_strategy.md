---
id: tbl_pbsdb_tb_pbs_bill_strategy
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
- tb_pbs_bill_strategy
subdomain: pricing
module: null
sensitivity: normal
name: 账单生成策略(tb_pbs_bill_strategy)
aliases:
- tb_pbs_bill_strategy
related_services:
- svc_pbs
related_scenarios: []
---
# 账单生成策略(tb_pbs_bill_strategy)

## 用途
账单生成策略。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BILL_STRATEGY_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `BILL_RANGE` | varchar(2) | NOT NULL | 1-单笔 2-周 3-月 4-年 5-扩展 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `MEMO` | varchar(300) |  | 备注 |
| `STATUS` | char | NOT NULL | 状态 C-创建 A-可用 D-废弃 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改人 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建人 |

## 主键 / 索引
- 主键:(`BILL_STRATEGY_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
