---
id: tbl_merchant_t_pay_link_status
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
- t_pay_link_status
subdomain: merchant
module: null
sensitivity: normal
name: pay link status table(t_pay_link_status)
aliases:
- t_pay_link_status
related_services:
- svc_merchant
related_scenarios: []
---
# pay link status table(t_pay_link_status)

## 用途
pay link status table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `merchant_id` | bigint | NOT NULL | merchant id |
| `merchant_mid` | varchar(32) | NOT NULL | merchant mid |
| `e_com_status` | varchar(10) | 默认 'DISABLED' | E-COM status |
| `pos_status` | varchar(10) | 默认 'DISABLED' | pos status |
| `created_time` | timestamp | NOT NULL | create time |
| `last_updated_time` | timestamp | NOT NULL | last update time |
| `data_version` | bigint | NOT NULL | data version |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `merchant_mid_idx` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
