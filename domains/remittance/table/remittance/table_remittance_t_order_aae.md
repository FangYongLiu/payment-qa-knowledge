---
id: tbl_remittance_t_order_aae
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_order_aae
subdomain: remittance
module: null
sensitivity: normal
name: AAE订单详情(t_order_aae)
aliases:
- t_order_aae
related_services:
- svc_remittance
related_scenarios: []
---
# AAE订单详情(t_order_aae)

## 用途
AAE订单详情。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `order_no` | bigint | PK / NOT NULL | 订单号 |
| `recipient_id` | varchar(32) | NOT NULL | 收款人 |
| `recipient_type` | varchar(10) | NOT NULL | 收款人类型: SELF= 自己,BUSINESS=企业,OTHER=其他 |
| `recipient_email` | varchar(32) |  | 收款人邮箱 |
| `bank_id` | varchar(32) | NOT NULL | 银行Id |
| `bank_name` | varchar(100) | NOT NULL | 银行名称 |
| `recipient_info` | varchar(1000) | NOT NULL | 收款人信息 |
| `additional_info` | varchar(1000) | NOT NULL | 汇款附属信息 |
| `service_fee` | decimal(19,4) |  | 服务费 |
| `vat` | decimal(19,4) |  | 增值税 |
| `verification_no` | varchar(32) |  | 渠道验证编码 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `rem_extension` | varchar(300) |  | 交易扩展参数 |
| `currency` | varchar(3) |  | 币种 |

## 主键 / 索引
- 主键:(`order_no`)
- 索引:
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
