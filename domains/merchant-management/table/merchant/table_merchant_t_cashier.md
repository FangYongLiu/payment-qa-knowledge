---
id: tbl_merchant_t_cashier
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
- t_cashier
subdomain: merchant
module: null
sensitivity: normal
name: 收银员(t_cashier)
aliases:
- t_cashier
related_services:
- svc_merchant
related_scenarios: []
---
# 收银员(t_cashier)

## 用途
收银员。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `merchant_id` | bigint | NOT NULL | 商户id |
| `merchant_mid` | varchar(32) | NOT NULL | 商户mid |
| `cashier_mid` | varchar(32) | NOT NULL | 收银员会员id |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_merchant_mid` 唯一 (merchant_mid, cashier_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
