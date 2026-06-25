---
id: tbl_acs_t_merchant_inner_account
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_merchant_inner_account
subdomain: acs
module: null
sensitivity: normal
name: 商户交易中间账户记录(t_merchant_inner_account)
aliases:
- t_merchant_inner_account
related_services:
- svc_acs
related_scenarios: []
---
# 商户交易中间账户记录(t_merchant_inner_account)

## 用途
商户交易中间账户记录。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `MERCHANT_INNER_ACCOUNT_ID` | decimal(8) | PK / NOT NULL | 记录ID |
| `MERCHANT_ID` | varchar(32) | NOT NULL | 商户号 |
| `ACCOUNT_NO` | varchar(128) | NOT NULL | 账户号 |
| `ACCOUNT_PLATFORM` | varchar(32) | NOT NULL | 账户模版所属平台 |
| `ACCOUNT_NAME` | varchar(128) |  | 账户名称 |
| `EXPRESSION` | varchar(256) |  | 表达试 |
| `TEMPLATE_ACCOUNT_ID` | decimal(8) | NOT NULL | 账户模版ID |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFY` | timestamp | NOT NULL | 修改时间 |
| `MEMO` | varchar(256) |  | 备注 |

## 主键 / 索引
- 主键:(`MERCHANT_INNER_ACCOUNT_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
