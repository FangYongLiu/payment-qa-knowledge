---
id: tbl_dpm_tb_title_stat
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- tb_title_stat
subdomain: dpm
module: null
sensitivity: normal
name: 科目统计信息(tb_title_stat)
aliases:
- tb_title_stat
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 科目统计信息(tb_title_stat)

## 用途
科目统计信息。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | leaf生成 |
| `account_time` | char(10) | NOT NULL | 周期开始时间 |
| `title_code` | varchar(16) | NOT NULL | 科目 |
| `currency` | char(3) | NOT NULL | 币种 |
| `balance_direction` | char | NOT NULL | 余额方向，0=共同,1=借方,2=贷方 |
| `debit_amount` | decimal(19,4) |  | 借方发生额 |
| `credit_amount` | decimal(19,4) |  | 贷方发生额 |
| `debit_count` | bigint |  | 借方发生笔数 |
| `credit_count` | bigint |  | 贷方发生笔数 |
| `debit_balance` | decimal(19,4) |  | 借方余额 |
| `credit_balance` | decimal(19,4) |  | 贷方余额 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modified` | timestamp |  | 最后修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_accounttime_titlecode` 唯一 (account_time, title_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
