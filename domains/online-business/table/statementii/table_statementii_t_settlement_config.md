---
id: tbl_statementii_t_settlement_config
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
- t_settlement_config
subdomain: statement
module: null
sensitivity: normal
name: 结算配置(t_settlement_config)
aliases:
- t_settlement_config
related_services:
- svc_statementii
related_scenarios: []
---
# 结算配置(t_settlement_config)

## 用途
结算配置。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `reserved_amount` | decimal(19,4) | NOT NULL | 预留金额 |
| `min_withdraw_amount` | decimal(19,4) |  | 最小提现金额 |
| `currency_code` | varchar(20) | NOT NULL | 币种 |
| `account_type` | varchar(20) | NOT NULL | 账户 |
| `status` | varchar(50) | NOT NULL | 状态  ENABLE 可用 INVALID 无效 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `beneficiary_type` | varchar(32) |  | 受益人类型 |
| `bankcard_no` | varchar(30) |  | 银行卡号 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_merchant_mid` 唯一 (merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
