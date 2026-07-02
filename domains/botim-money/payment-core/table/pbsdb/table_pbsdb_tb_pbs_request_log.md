---
id: tbl_pbsdb_tb_pbs_request_log
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
- tb_pbs_request_log
subdomain: pricing
module: null
sensitivity: normal
name: 计费请求日志表(tb_pbs_request_log)
aliases:
- tb_pbs_request_log
related_services:
- svc_pbs
related_scenarios: []
---
# 计费请求日志表(tb_pbs_request_log)

## 用途
计费请求日志表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `LOG_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `REQUEST_ID` | varchar(32) |  | 请求类型 |
| `REQUEST_TYPE` | decimal(1) |  | 请求类型 1-算费 2-计费 |
| `BIZ_NO` | varchar(32) |  | 订单流水号 |
| `POSTING_CODE` | varchar(100) |  | 业务子代码 |
| `AMOUNT` | decimal(15,4) |  | 计费金额 |
| `GMT_TRANSACTION` | timestamp |  | 交易时间 |
| `PAYER_PT` | varchar(100) |  | 交易付款方PT |
| `PAYEE_PT` | varchar(100) |  | 交易收款方PT |
| `CHANNEL` | varchar(32) |  | 渠道 |
| `CLIENT_APP_ID` | varchar(2) |  | 客户端应用标号 |
| `GMT_CREATE` | timestamp |  | 日志创建时间 |

## 主键 / 索引
- 主键:(`LOG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
