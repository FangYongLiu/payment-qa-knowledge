---
id: tbl_pbsdb_tb_pbs_error_monitor
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
- tb_pbs_error_monitor
subdomain: pricing
module: null
sensitivity: normal
name: 错误监控(tb_pbs_error_monitor)
aliases:
- tb_pbs_error_monitor
related_services:
- svc_pbs
related_scenarios: []
---
# 错误监控(tb_pbs_error_monitor)

## 用途
错误监控。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL | ID |
| `TYPE` | char(2) | NOT NULL | 错误类型 |
| `PAYMENT_SEQ_NO` | varchar(64) |  | 支付流水号 |
| `MEMBER_ID` | varchar(64) |  | 会员ID |
| `PROD_CODE` | varchar(32) |  | 产品编码 |
| `PAYMENT_CODE` | varchar(32) |  | 支付编码 |
| `PAYMENT_TIME` | timestamp |  | 支付时间 |
| `FUNDS_CHANNEL` | varchar(32) |  | 支付渠道 |
| `AMOUNT` | decimal(15,2) |  | 金额 |
| `MESSAGE_INFO` | varchar(4000) |  | 错误消息 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `ORIGINAL_REQUEST_DATA` | varchar(1024) |  | 错误描述 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
