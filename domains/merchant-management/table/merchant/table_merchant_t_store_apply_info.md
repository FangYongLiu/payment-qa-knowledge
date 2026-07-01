---
id: tbl_merchant_t_store_apply_info
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
- t_store_apply_info
subdomain: merchant
module: null
sensitivity: normal
name: 门店申请信息(t_store_apply_info)
aliases:
- t_store_apply_info
related_services:
- svc_merchant
related_scenarios: []
---
# 门店申请信息(t_store_apply_info)

## 用途
门店申请信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `merchant_creation_id` | bigint | PK / AUTO_INC | 商户创建id |
| `name` | varchar(64) | NOT NULL | 门店名称 |
| `apply_device_number` | int | NOT NULL | 申请设备数量 |
| `apply_device_type` | varchar(32) | NOT NULL | 申请设备型号 BOX 小白盒 SMART_POS 智能pos |
| `location` | varchar(64) | NOT NULL | 门店地址 |
| `store_entrance_photo_path` | varchar(200) | NOT NULL | 门头照路径 |
| `cash_desk_photo_path` | varchar(200) | NOT NULL | 收银台照路径 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`merchant_creation_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
