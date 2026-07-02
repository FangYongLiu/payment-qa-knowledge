---
id: tbl_merchant_t_merchant_wps_info
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
- t_merchant_wps_info
subdomain: merchant
module: null
sensitivity: normal
name: 商户wps信息表(t_merchant_wps_info)
aliases:
- t_merchant_wps_info
related_services:
- svc_merchant
related_scenarios: []
---
# 商户wps信息表(t_merchant_wps_info)

## 用途
商户wps信息表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `merchant_creation_id` | bigint | NOT NULL | 商户创建id |
| `merchant_mid` | varchar(50) |  | 商户id |
| `company_classification` | varchar(32) |  | Company Category |
| `free_zone` | varchar(32) |  | Free zone |
| `company_free_zone_number` | varchar(50) |  | Free zone Account Number |
| `supported_program` | varchar(32) |  | Supported Program |
| `company_mol_id` | varchar(50) |  | Company MOL ID |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_mid` 唯一 (merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
