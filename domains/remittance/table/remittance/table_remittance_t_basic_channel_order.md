---
id: tbl_remittance_t_basic_channel_order
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
- t_basic_channel_order
subdomain: remittance
module: null
sensitivity: normal
name: 渠道订单(t_basic_channel_order)
aliases:
- t_basic_channel_order
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道订单(t_basic_channel_order)

## 用途
渠道订单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `basic_order_no` | bigint | PK / NOT NULL | 汇款订单号 |
| `channel_code` | varchar(32) | NOT NULL | 渠道code |
| `recipient_id` | bigint | NOT NULL | 收款人受益人ID;对应渠道用户ID |
| `quote_id` | varchar(64) |  | 渠道汇率ID |
| `quote_rate` | decimal(15,8) |  | 成本汇率;从外部渠道查询的实时汇率 |
| `bank_code` | varchar(30) |  | 银行CODE |
| `bank_name` | varchar(100) |  | 银行名称 |
| `wallet_name` | varchar(100) |  | 钱包名称 |
| `wallet_code` | varchar(32) |  | 钱包code |
| `account_no` | varchar(100) |  | 收款账号 |
| `iban` | varchar(32) |  | iban |
| `service_fee` | decimal(15,4) |  | 服务费 |
| `vat` | decimal(15,4) |  | 税 |
| `source_income` | varchar(32) |  | 收入来源 |
| `purpose` | varchar(100) |  | 目的 |
| `channel_param_info` | varchar(900) |  | 转换后的渠道参数 |
| `channel_expire_time` | timestamp |  | 渠道订单过期时间;渠道订单返回的过期时间 |
| `additional_info` | varchar(255) |  | 补充信息 |
| `txn_type` | varchar(12) |  | 汇款清算类型 |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `recipient_vat` | decimal(15,4) |  | 收款税 |
| `recipient_fee` | decimal(15,4) |  | 收款费用 |
| `recipient_fee_currency` | char(3) |  | 收款方费用币种 |
| `estimated_info` | varchar(255) |  | 预估信息 |

## 主键 / 索引
- 主键:(`basic_order_no`)
- 索引:
  - `idx_basic_c_qid_c_code` (quote_id, channel_code)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
