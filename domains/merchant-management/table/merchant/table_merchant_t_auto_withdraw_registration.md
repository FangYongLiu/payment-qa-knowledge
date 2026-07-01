---
id: tbl_merchant_t_auto_withdraw_registration
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_auto_withdraw_registration
subdomain: merchant
module: null
sensitivity: normal
name: 自动提现注册(t_auto_withdraw_registration)
aliases:
- t_auto_withdraw_registration
related_services:
- svc_merchant
related_scenarios: []
---
# 自动提现注册(t_auto_withdraw_registration)

## 用途
自动提现注册。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | registration id |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `daily_remain_amount` | decimal(19,4) | NOT NULL | 每日预留金额 |
| `currency_code` | varchar(20) | NOT NULL | 币种 |
| `account_type` | varchar(20) | NOT NULL | 账户 |
| `status` | varchar(32) | NOT NULL | 状态 ENABLE 有效 INVALID 无效 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
