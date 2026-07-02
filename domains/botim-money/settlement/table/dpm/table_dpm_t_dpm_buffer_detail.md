---
id: tbl_dpm_t_dpm_buffer_detail
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
- t_dpm_buffer_detail
subdomain: dpm
module: null
sensitivity: normal
name: 待缓冲入账明细(缓冲池)(t_dpm_buffer_detail)
aliases:
- t_dpm_buffer_detail
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 待缓冲入账明细(缓冲池)(t_dpm_buffer_detail)

## 用途
待缓冲入账明细(缓冲池)。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BUFFER_DETAIL_ID` | decimal(32) | PK / NOT NULL | 待入账数据流水号 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账户号 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪号 |
| `VOUCHER_NO` | varchar(50) | NOT NULL | 凭证号 |
| `TRANSACTION_NO` | varchar(32) | NOT NULL | 事务号 |
| `CURRENCY` | char(3) | NOT NULL | 币种 |
| `AMOUNT` | decimal(19,4) | NOT NULL | 金额 |
| `CRDR` | decimal(1) | NOT NULL | 借贷方向 1:借 2:贷 |
| `TXN_TYPE` | decimal(1) | NOT NULL | 交易类型 0:正常 1:红字 2:蓝字 9:抹帐 |
| `ACCOUNTING_RULE` | decimal(1) | NOT NULL | 分户执行顺序 0.先贷后借(默认) 1.借记 2.贷记 |
| `PRODUCT_CODE` | varchar(12) |  | PE产品编码 |
| `PAY_CODE` | varchar(12) |  | PE支付编码 |
| `STATUS` | decimal(1) | NOT NULL | 状态 0.待入账 1.成功 2.失败 3.处理中 |
| `COUNT` | decimal(1) | NOT NULL | 执行次数 |
| `SUMMARY` | varchar(256) |  | 摘要 |
| `OCCUPY_SIGN` | varchar(32) |  | 时间戳 |
| `REMARK` | varchar(256) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |
| `SUITE_NO` | varchar(32) | NOT NULL | 套号 |
| `CONTEXT_VOUCHER_NO` | varchar(32) |  | 关联凭证号 |
| `ACCOUNTING_DATE` | varchar(8) |  | 会计日 |
| `OPERATION_TYPE` | decimal(1) |  | 操作类型 |
| `BALANCE_TYPE` | decimal(1) |  | 余额类型 |
| `PAYMENT_VOUCHER_NO` | varchar(64) |  | 支付凭证号 |
| `CLEARING_CODE` | varchar(32) |  | 清算编码 |
| `extension` | varchar(255) |  | 扩展信息 |

## 主键 / 索引
- 主键:(`BUFFER_DETAIL_ID`)
- 索引:
  - `IDX_BUFFERDETAIL_CT` (CREATE_TIME)
  - `IDX_DBD_TRANSACTION_NO` (TRANSACTION_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
