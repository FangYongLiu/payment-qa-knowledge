---
id: tbl_aml_t_freeze_order
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_freeze_order
subdomain: aml
module: null
sensitivity: normal
name: 冻结订单表(t_freeze_order)
aliases:
- t_freeze_order
related_services:
- svc_aml
related_scenarios: []
---
# 冻结订单表(t_freeze_order)

## 用途
冻结订单表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `payment_order_no` | bigint | PK / NOT NULL | 支付订单号 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `account_no` | varchar(30) | NOT NULL | 会员账号 |
| `freeze_amount` | decimal(19,4) | NOT NULL | 冻结金额 |
| `unfreeze_amount` | decimal(19,4) | NOT NULL | 已解冻金额 |
| `currency` | char(3) | NOT NULL | 币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `status` | varchar(10) | NOT NULL | 状态：Freeze=冻结中，Unfreeze=已解冻 |
| `extension` | varchar(255) |  | 扩展参数 |
| `memo` | varchar(255) |  | 备注 |
| `freeze_time` | timestamp(3) | NOT NULL | 冻结时间 |
| `operator` | varchar(30) | NOT NULL | 操作人 |
| `task_no` | bigint |  | task no |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL | 修改时间 |
| `client_id` | varchar(30) | NOT NULL | 调用端id |

## 主键 / 索引
- 主键:(`payment_order_no`)
- 索引:
  - `idx_freeze_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
