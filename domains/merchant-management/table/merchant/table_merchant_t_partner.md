---
id: tbl_merchant_t_partner
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
- t_partner
subdomain: merchant
module: null
sensitivity: normal
name: 合伙人表(t_partner)
aliases:
- t_partner
related_services:
- svc_merchant
related_scenarios: []
---
# 合伙人表(t_partner)

## 用途
合伙人表。属 merchant 库,由 [[svc_merchant]] 读写。

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
| `partner_type` | varchar(32) | NOT NULL | 合伙人类型：SHARE_HOLDER(股东/合伙人), SIGNATORY(法人/签字人) |
| `full_name` | varchar(200) | NOT NULL | 姓名全称 |
| `gender` | varchar(32) |  | 性别 |
| `country` | varchar(50) |  | 国家 |
| `country_code` | varchar(5) |  | 国家代码 |
| `birthdate` | datetime |  | 出生日期 |
| `share_proportion` | varchar(10) |  | 股权占比 |
| `title` | varchar(50) |  | 职务头衔 |
| `id_num` | varchar(32) | NOT NULL | 证件号码 |
| `id_type` | varchar(32) | NOT NULL | 证件类型 |
| `cert_front_file_path` | varchar(64) | NOT NULL | 证件前照文件 |
| `cert_back_file_path` | varchar(64) |  | 证件后照文件 |
| `id_expire_date` | datetime | NOT NULL | 证件失效日期 |
| `contact_mobile` | varchar(20) |  | 联系人手机 |
| `contact_email` | varchar(100) |  | 联系人邮箱 |
| `auth_letter_file_path` | varchar(80) |  | 授权书 |
| `power_attorney_file_path` | varchar(100) |  | 委托书 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `designation` | varchar(32) |  | Designation |
| `channel_of_delivery` | varchar(100) |  | Channel of delivery |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UK_CERT_NO` 唯一 (id_num, partner_type, merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
