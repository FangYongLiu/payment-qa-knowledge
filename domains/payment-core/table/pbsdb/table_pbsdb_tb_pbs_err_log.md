---
id: tbl_pbsdb_tb_pbs_err_log
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
- tb_pbs_err_log
subdomain: pricing
module: null
sensitivity: normal
name: 错误日志表(tb_pbs_err_log)
aliases:
- tb_pbs_err_log
related_services:
- svc_pbs
related_scenarios: []
---
# 错误日志表(tb_pbs_err_log)

## 用途
错误日志表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ERR_LOG_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `ERR_TYPE` | varchar(2) |  | 错误类型 |
| `ERR_CODE` | varchar(100) |  | 错误编码 |
| `ERR_DESC` | varchar(1000) |  | 错误说明 |
| `BILL_WORORDER_ID` | decimal(15) |  | 工单ID |
| `BILL_ID` | decimal(15) |  | 账单ID |
| `GMT_CREATE` | timestamp |  | 日志创建时间 |

## 主键 / 索引
- 主键:(`ERR_LOG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
