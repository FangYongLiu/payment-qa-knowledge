---
id: tbl_statementii_t_settlement_config_bak
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (statementii schema) 2026-06-25
tags:
- statementii
- statement
- t_settlement_config_bak
subdomain: statement
module: null
sensitivity: normal
name: 结算配置备份(t_settlement_config_bak)
aliases:
- t_settlement_config_bak
related_services:
- svc_statementii
related_scenarios: []
---
# 结算配置备份(t_settlement_config_bak)

## 用途
结算配置备份。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `reserved_amount` | decimal(19,4) | NOT NULL | 预留金额 |
| `min_withdraw_amount` | decimal(19,4) |  | 最小提现金额 |
| `currency_code` | char(3) | NOT NULL | 币种 |
| `account_type` | varchar(20) | NOT NULL | 账户 |
| `start_time` | time |  | 开始时间, 到小时 |
| `beneficiary_type` | varchar(32) |  |  |
| `bankcard_no` | varchar(20) |  | 银行卡号 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
