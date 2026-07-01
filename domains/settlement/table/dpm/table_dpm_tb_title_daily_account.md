---
id: tbl_dpm_tb_title_daily_account
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
- tb_title_daily_account
subdomain: dpm
module: null
sensitivity: normal
name: 账户科目每日信息(tb_title_daily_account)
aliases:
- tb_title_daily_account
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 账户科目每日信息(tb_title_daily_account)

## 用途
账户科目每日信息。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL |  |
| `ACCOUNT_DATE` | char(8) | NOT NULL | 会计日 |
| `TITLE_CODE` | varchar(16) | NOT NULL | 科目代码 |
| `BALANCE_DIRECTION` | char | NOT NULL | 余额方向 |
| `DEBIT_AMOUNT` | decimal(19,4) |  | 借方发生额 |
| `CREDIT_AMOUNT` | decimal(19,4) |  | 贷方发生额 |
| `DEBIT_COUNT` | decimal(15) |  | 借方发生笔数 |
| `CREDIT_COUNT` | decimal(15) |  | 贷方发生笔数 |
| `DEBIT_BALANCE` | decimal(19,4) |  | 借方余额 |
| `CREDIT_BALANCE` | decimal(19,4) |  | 贷方余额 |
| `CURRENCY` | decimal(3) | NOT NULL | 币种 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 最后修改时间 |
| `ACCOUNT_NO` | varchar(32) |  | 账户代码 |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `U_TITLE_DAILY_DATE_ACCT` 唯一 (TITLE_CODE, ACCOUNT_DATE, ACCOUNT_NO)
- 索引:
  - `IDX_TD_ACCOUNT_DATE_ACCT` (ACCOUNT_DATE)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
