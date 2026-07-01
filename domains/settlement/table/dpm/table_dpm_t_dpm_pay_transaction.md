---
id: tbl_dpm_t_dpm_pay_transaction
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
- t_dpm_pay_transaction
subdomain: dpm
module: null
sensitivity: normal
name: 入账事务(t_dpm_pay_transaction)
aliases:
- t_dpm_pay_transaction
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 入账事务(t_dpm_pay_transaction)

## 用途
入账事务。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRANSACTION_ID` | varchar(32) | PK / NOT NULL | 事务ID |
| `PACKAGE_NO` | varchar(32) |  | 包号，批量入帐时用 |
| `TRANSACTION_NO` | varchar(32) | NOT NULL | 事务流水号(PE支付流水号) |
| `APP_ID` | varchar(10) |  | 应用ID |
| `SYS_TRACE_NO` | varchar(32) |  | 入账请求流水号(CS清算ID) |
| `TXN_TYPE` | decimal(1) | NOT NULL | 0:正常 1:红字 2:蓝字 9:抹帐 |
| `PRODUCT_CODE` | varchar(12) |  | PE产品编码 |
| `PAY_CODE` | varchar(12) |  | PE支付编码 |
| `STATUS` | decimal(1) | NOT NULL | 0:初始 1:处理中 2:入账完成(成功) 3:入账失败,处理中 4:入账完成(失败) |
| `ACCOUNTING_DATE` | varchar(8) | NOT NULL | 会计日 |
| `CREATE_TIME` | timestamp | NOT NULL | 插入时间 |
| `LAST_UPDATE_TIME` | timestamp |  | 更新时间 |
| `REMARK` | varchar(256) |  | 备注 |
| `CONTEXT_TRANS_NO` | varchar(32) |  | 关联事务号，回滚用? |

## 主键 / 索引
- 主键:(`TRANSACTION_ID`)
- 唯一约束:
  - `UDX_PAYSEQNO_CLEARINGNO` 唯一 (TRANSACTION_NO)
- 索引:
  - `IDX_DPT_TO` (SYS_TRACE_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
