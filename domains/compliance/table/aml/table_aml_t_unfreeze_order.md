---
id: tbl_aml_t_unfreeze_order
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
- t_unfreeze_order
subdomain: aml
module: null
sensitivity: normal
name: 解冻订单表(t_unfreeze_order)
aliases:
- t_unfreeze_order
related_services:
- svc_aml
related_scenarios: []
---
# 解冻订单表(t_unfreeze_order)

## 用途
解冻订单表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `payment_order_no` | bigint | PK / NOT NULL | 支付订单号 |
| `freeze_order_no` | bigint | NOT NULL | 原冻结订单号 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `account_no` | varchar(30) | NOT NULL | 会员账号 |
| `unfreeze_amount` | decimal(19,4) |  | 解冻金额 |
| `currency` | char(3) | NOT NULL | 币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `memo` | varchar(255) |  | 备注 |
| `unfreeze_time` | timestamp(3) | NOT NULL | 解冻时间 |
| `operator` | varchar(30) | NOT NULL | 操作人 |
| `client_id` | varchar(30) | NOT NULL | 调用端id |

## 主键 / 索引
- 主键:(`payment_order_no`)
- 索引:
  - `idx_freeze_order_no` (freeze_order_no)
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
