---
id: tbl_dpm_t_dpm_outer_account_diary
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
- t_dpm_outer_account_diary
subdomain: dpm
module: null
sensitivity: normal
name: 外部账户日记账(t_dpm_outer_account_diary)
aliases:
- t_dpm_outer_account_diary
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 外部账户日记账(t_dpm_outer_account_diary)

## 用途
外部账户日记账。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ACCOUNT_NO` | varchar(32) | PK / NOT NULL | ACCOUNT_NO |
| `ACCOUNT_DATE` | varchar(8) | PK / NOT NULL | ACCOUNT_DATE |
| `BEGIN_DR_BAL` | decimal(19,4) | 默认 0 | BEGIN_DR_BAL |
| `BEGIN_CR_BAL` | decimal(19,4) | 默认 0 | BEGIN_CR_BAL |
| `BEGIN_DR_AVAIL_BAL` | decimal(19,4) | 默认 0 | BEGIN_DR_AVAIL_BAL |
| `BEGIN_CR_AVAIL_BAL` | decimal(19,4) | 默认 0 | BEGIN_CR_AVAIL_BAL |
| `DEBIT_AMT` | decimal(19,4) | 默认 0 | DEBIT_AMT |
| `CREDIT_AMT` | decimal(19,4) | 默认 0 | CREDIT_AMT |
| `DEBIT_CNT` | decimal | 默认 0 | DEBIT_CNT |
| `CREDIT_CNT` | decimal | 默认 0 | CREDIT_CNT |
| `DEBIT_FROZEN_AMT` | decimal(19,4) | 默认 0 | DEBIT_FROZEN_AMT |
| `CREDIT_FROZEN_AMT` | decimal(19,4) | 默认 0 | CREDIT_FROZEN_AMT |
| `DEBIT_FROZEN_CNT` | decimal | 默认 0 | DEBIT_FROZEN_CNT |
| `CREDIT_FROZEN_CNT` | decimal | 默认 0 | CREDIT_FROZEN_CNT |
| `DEBIT_UNFROZEN_AMT` | decimal(19,4) | 默认 0 | DEBIT_UNFROZEN_AMT |
| `CREDIT_UNFROZEN_AMT` | decimal(19,4) | 默认 0 | CREDIT_UNFROZEN_AMT |
| `DEBIT_UNFROZEN_CNT` | decimal | 默认 0 | DEBIT_UNFROZEN_CNT |
| `CREDIT_ENFROZEN_CNT` | decimal | 默认 0 | CREDIT_ENFROZEN_CNT |
| `END_DR_BAL` | decimal(19,4) | 默认 0 | END_DR_BAL |
| `END_CR_BAL` | decimal(19,4) | 默认 0 | END_CR_BAL |
| `END_DR_AVAIL_BAL` | decimal(19,4) | 默认 0 | END_DR_AVAIL_BAL |
| `END_CR_AVAIL_BAL` | decimal(19,4) | 默认 0 | END_CR_AVAIL_BAL |
| `IS_FINAL` | decimal(1) |  | 0:已经扎帐 1:未扎帐 |
| `CREATE_TIME` | timestamp |  | CREATE_TIME |
| `LAST_UPDATE_TIME` | timestamp |  | LAST_UPDATE_TIME |

## 主键 / 索引
- 主键:(`ACCOUNT_NO`, `ACCOUNT_DATE`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
