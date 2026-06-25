---
id: tbl_statementii_t_settlement_order
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
- t_settlement_order
subdomain: statement
module: null
sensitivity: normal
name: 结算订单(t_settlement_order)
aliases:
- t_settlement_order
related_services:
- svc_statementii
related_scenarios: []
---
# 结算订单(t_settlement_order)

## 用途
结算订单。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | order id |
| `fos_voucher_no` | varchar(50) |  | 提现订单号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `currency_code` | varchar(20) | NOT NULL | 币种 |
| `amount` | decimal(19,4) | NOT NULL | 提现金额 |
| `card_id` | varchar(20) |  | 卡ID |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建；STARTED 已开始；PROCESSING 处理中; FAIL 失败 SUCCESS 成功 |
| `error_code` | varchar(50) |  | 错误码 |
| `error_message` | varchar(500) |  | 错误信息 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `task_id` | bigint | NOT NULL | 任务id |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_task_id` 唯一 (task_id)
- 索引:
  - `idx_merchant_mid` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
