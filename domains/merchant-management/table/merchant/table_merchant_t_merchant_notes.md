---
id: tbl_merchant_t_merchant_notes
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
- t_merchant_notes
subdomain: merchant
module: null
sensitivity: normal
name: 商户备注(t_merchant_notes)
aliases:
- t_merchant_notes
related_services:
- svc_merchant
related_scenarios: []
---
# 商户备注(t_merchant_notes)

## 用途
商户备注。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `merchant_mid` | varchar(50) |  | 商户id |
| `note` | varchar(512) |  | 备注 |
| `creator` | varchar(50) |  | 创建人 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `IDX_MERCHANT_NOTES_MERCHANT_MID` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
