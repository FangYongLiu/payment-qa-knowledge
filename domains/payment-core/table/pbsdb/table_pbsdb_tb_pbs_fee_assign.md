---
id: tbl_pbsdb_tb_pbs_fee_assign
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
- tb_pbs_fee_assign
subdomain: pricing
module: null
sensitivity: normal
name: 分摊分润策略表(tb_pbs_fee_assign)
aliases:
- tb_pbs_fee_assign
related_services:
- svc_pbs
related_scenarios: []
---
# 分摊分润策略表(tb_pbs_fee_assign)

## 用途
分摊分润策略表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ASSIGN_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `CRITERION_ID` | decimal(15) |  | 约束ID，暂不起作用 |
| `ORI_POSTING_CODE` | varchar(32) | NOT NULL | 原业务子代码 |
| `ASSIGN_FLAG` | varchar(2) | NOT NULL | 分润分摊标志 R-分润 T-分摊 G-共同 |
| `MEMO` | varchar(300) |  | 描述 |
| `STATUS` | char | NOT NULL | C-创建 A-可用 D-废弃 |
| `EXPIREDATE` | timestamp | NOT NULL | 失效时间 |
| `VALIDDATE` | timestamp | NOT NULL | 生效时间 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`ASSIGN_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
