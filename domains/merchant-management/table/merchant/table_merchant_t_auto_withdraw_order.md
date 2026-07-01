---
id: tbl_merchant_t_auto_withdraw_order
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
- t_auto_withdraw_order
subdomain: merchant
module: null
sensitivity: normal
name: 自动提现订单(t_auto_withdraw_order)
aliases:
- t_auto_withdraw_order
related_services:
- svc_merchant
related_scenarios: []
---
# 自动提现订单(t_auto_withdraw_order)

## 用途
自动提现订单。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | order id |
| `fos_voucher_no` | varchar(32) |  | 提现订单号 |
| `period_id` | bigint | NOT NULL | 账期ID |
| `registration_id` | bigint | NOT NULL | 注册ID |
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

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_mid` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
