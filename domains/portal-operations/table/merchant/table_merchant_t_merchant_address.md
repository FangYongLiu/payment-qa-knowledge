---
id: tbl_merchant_t_merchant_address
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_merchant_address
subdomain: merchant
module: null
sensitivity: normal
name: 商户地址表(t_merchant_address)
aliases:
- t_merchant_address
related_services:
- svc_merchant
related_scenarios: []
---
# 商户地址表(t_merchant_address)

## 用途
商户地址表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `merchant_creation_id` | bigint | NOT NULL | 商户创建id |
| `merchant_mid` | varchar(50) |  | 商户id |
| `type` | varchar(32) | NOT NULL | 类型：REGISTER(注册地址), BUSINESS(运营地址) |
| `office_no` | varchar(32) | NOT NULL | 编号 |
| `building_name` | varchar(255) | NOT NULL | 大楼名称 |
| `area` | varchar(50) | NOT NULL | 区域 |
| `city` | varchar(50) | NOT NULL | 城市 |
| `country` | varchar(50) | NOT NULL | 国家 |
| `country_code` | varchar(5) | NOT NULL | 国家代码 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_creation_id` (merchant_creation_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
