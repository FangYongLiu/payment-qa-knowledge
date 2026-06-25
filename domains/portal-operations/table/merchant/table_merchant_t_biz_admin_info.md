---
id: tbl_merchant_t_biz_admin_info
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
- t_biz_admin_info
subdomain: merchant
module: null
sensitivity: normal
name: 业务管理员信息表(t_biz_admin_info)
aliases:
- t_biz_admin_info
related_services:
- svc_merchant
related_scenarios: []
---
# 业务管理员信息表(t_biz_admin_info)

## 用途
业务管理员信息表。属 merchant 库,由 [[svc_merchant]] 读写。

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
| `biz_type` | varchar(32) | NOT NULL | 业务类型：SUPPER_ADMIN(超级管理员),ACQUIRE_ADMIN(收单服务管理员),WPS_ADMIN(WPS服务管理员) |
| `full_name` | varchar(200) | NOT NULL | 姓名全称 |
| `id_type` | varchar(32) | NOT NULL | 证件类型 |
| `id_num` | varchar(32) | NOT NULL | 证件号码 |
| `cert_front_file_path` | varchar(64) | NOT NULL | 证件前照文件 |
| `cert_back_file_path` | varchar(64) |  | 证件后照文件 |
| `id_expire_date` | datetime | NOT NULL | 证件失效日期 |
| `contact_mobile` | varchar(20) |  | 联系人手机 |
| `contact_email` | varchar(100) |  | 联系人邮箱 |
| `auth_letter_file_path` | varchar(80) | NOT NULL | 授权书 |
| `power_attorney_file_path` | varchar(100) |  | 委托书 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `designation` | varchar(32) |  | Designation |
| `country` | varchar(50) |  | Country of admin |
| `birthdate` | varchar(10) |  | Birthdate of admin |
| `gender` | varchar(10) |  | Gender of admin |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UK_CERT_NO` 唯一 (id_num, biz_type, id_type, merchant_mid)
- 索引:
  - `idx_merchant_creation_id` (merchant_creation_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
