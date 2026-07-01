---
id: tbl_dpm_t_dpm_buffer_detail_log
object_type: Table
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- t_dpm_buffer_detail_log
subdomain: dpm
module: null
sensitivity: normal
name: 待缓冲入账明细(缓冲池)日志(t_dpm_buffer_detail_log)
aliases:
- t_dpm_buffer_detail_log
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 待缓冲入账明细(缓冲池)日志(t_dpm_buffer_detail_log)

## 用途
待缓冲入账明细(缓冲池)日志。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BUFFER_DETAIL_ID` | decimal(32) | PK / NOT NULL | 待入账数据流水号 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账户号 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪号 |
| `VOUCHER_NO` | varchar(50) | NOT NULL | 凭证号 |
| `TRANSACTION_NO` | varchar(32) | NOT NULL | 事务号 |
| `AMOUNT` | decimal(19,4) | NOT NULL | 金额 |
| `currency` | char(3) |  | 币种 |
| `CRDR` | decimal(1) | NOT NULL | 借贷方向 1:借 2:贷 |
| `TXN_TYPE` | decimal(1) | NOT NULL | 交易类型 0:正常 1:红字 2:蓝字 9:抹帐 |
| `ACCOUNTING_RULE` | decimal(1) | NOT NULL | 分户执行顺序 0.先贷后借(默认) 1.借记 2.贷记 |
| `PRODUCT_CODE` | varchar(12) |  | PE产品编码 |
| `PAY_CODE` | varchar(12) |  | PE支付编码 |
| `SUMMARY` | varchar(256) |  | 摘要 |
| `REMARK` | varchar(256) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |
| `SUITE_NO` | varchar(32) | NOT NULL | 套号 |
| `CONTEXT_VOUCHER_NO` | varchar(32) |  | 关联凭证号 |
| `ACCOUNTING_DATE` | varchar(8) |  | 会计日 |
| `OPERATION_TYPE` | decimal(1) |  | 操作类型 |
| `BALANCE_TYPE` | decimal(1) |  | 余额类型 |

## 主键 / 索引
- 主键:(`BUFFER_DETAIL_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
