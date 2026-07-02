---
id: tbl_dpm_tb_title_daily
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
- tb_title_daily
subdomain: dpm
module: null
sensitivity: normal
name: 科目每日信息(tb_title_daily)
aliases:
- tb_title_daily
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 科目每日信息(tb_title_daily)

## 用途
科目每日信息。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL | ID |
| `ACCOUNT_DATE` | char(8) | NOT NULL | 会计日 |
| `TITLE_CODE` | varchar(16) | NOT NULL | 科目代码 |
| `CURRENCY` | char(3) | NOT NULL | 币种 |
| `BALANCE_DIRECTION` | char | NOT NULL | 余额方向 |
| `DEBIT_AMOUNT` | decimal(19,4) |  | 借方发生额 |
| `CREDIT_AMOUNT` | decimal(19,4) |  | 贷方发生额 |
| `DEBIT_COUNT` | decimal(15) |  | 借方发生笔数 |
| `CREDIT_COUNT` | decimal(15) |  | 贷方发生笔数 |
| `DEBIT_BALANCE` | decimal(19,4) |  | 借方余额 |
| `CREDIT_BALANCE` | decimal(19,4) |  | 贷方余额 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 最后修改时间 |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `uk_accountdate_titlecode` 唯一 (ACCOUNT_DATE, TITLE_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
