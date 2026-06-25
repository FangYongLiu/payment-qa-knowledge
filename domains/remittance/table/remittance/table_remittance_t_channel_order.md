---
id: tbl_remittance_t_channel_order
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
- t_channel_order
subdomain: remittance
module: null
sensitivity: normal
name: 渠道订单(t_channel_order)
aliases:
- t_channel_order
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道订单(t_channel_order)

## 用途
渠道订单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `order_no` | bigint | PK / NOT NULL | 汇款订单号 |
| `org_order_no` | bigint |  | 原汇款订单号 |
| `channel_code` | varchar(32) | NOT NULL | 渠道code |
| `recipient_id` | bigint | NOT NULL | 收款人受益人ID;对应渠道用户ID |
| `reference_number` | varchar(64) |  | 渠道reference number |
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
| `next_retry_time` | timestamp |  | 下次执行时间 |
| `retry_times` | int |  | 重试次数 |
| `communication_status` | char |  | 状态(I:初始化,S:成功,F:失败,E:异常) |
| `channel_order_no` | varchar(64) |  | 渠道订单号 |
| `remittance_create_time` | varchar(35) |  | 汇款创建时间 |
| `api_result_code` | varchar(32) |  | api retrun code |
| `api_result_sub_code` | varchar(32) |  | api retrun sub code |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `recipient_vat` | decimal(15,4) |  | 收款税 |
| `recipient_fee` | decimal(15,4) |  | 收款费用 |
| `recipient_fee_currency` | char(3) |  | Recipient fee currency |
| `estimated_info` | varchar(255) |  | 预估信息 |

## 主键 / 索引
- 主键:(`order_no`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
