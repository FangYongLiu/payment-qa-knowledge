---
id: tbl_merchant_t_store
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
- t_store
subdomain: merchant
module: null
sensitivity: normal
name: 门店(t_store)
aliases:
- t_store
related_services:
- svc_merchant
related_scenarios: []
---
# 门店(t_store)

## 用途
门店。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 门店id，主键 |
| `merchant_id` | bigint | NOT NULL | 商户id |
| `status` | varchar(50) | NOT NULL | 状态 CREATED 已创建 |
| `name` | varchar(200) | NOT NULL | 门店名称 |
| `location` | varchar(200) |  | 地点 |
| `store_entrance_photo_path` | varchar(200) |  | 门头照路径 |
| `cash_desk_photo_path` | varchar(200) |  | 收银台照路径 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `longitude` | decimal(15,10) |  | 经度 |
| `latitude` | decimal(15,10) |  | 纬度 |
| `nation` | varchar(50) |  | 国家 |
| `city` | varchar(50) |  | 城市 |
| `contact_mobile` | varchar(20) |  | 联系人手机号 |
| `eatm_switch` | varchar(10) |  | eatm开关 ON OFF |
| `address_line1` | varchar(200) |  | address line1 |
| `address_line2` | varchar(200) |  | address line2 |
| `address_line3` | varchar(200) |  | address line3 |
| `aplus_approve_result` | varchar(20) |  | 阿里审核状态 |
| `aplus_approve_reject_reason` | varchar(500) |  | 阿里审核驳回备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
