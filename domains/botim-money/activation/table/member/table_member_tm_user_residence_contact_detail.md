---
id: tbl_member_tm_user_residence_contact_detail
object_type: Table
name: Customer Residence and Contact Info (tm_user_residence_contact_detail)
aliases: [tm_user_residence_contact_detail, member.tm_user_residence_contact_detail]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: member schema DDL
tags: [activation, member]
sensitivity: normal
related_services: []
---

# Customer Residence and Contact Info (tm_user_residence_contact_detail)

## 用途
物理表 `member.tm_user_residence_contact_detail`,主键 `id`。Customer Residence and Contact Info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `entity_id` | bigint | Entity ID |
| `issue_date` | datetime | Issue Date · 可空 |
| `document_no` | varchar(50) | Document No · 可空 |
| `expiry_date` | date | Expiry Date · 可空 |
| `sponsor_name_ar` | varchar(255) | Sponsor Name Ar · 可空 |
| `sponsor_name_en` | varchar(255) | Sponsor Name En · 可空 |
| `emirates_id_number` | varchar(50) | Emirates ID Number · 可空 |
| `residence_class_ar` | varchar(100) | Residence Class Ar · 可空 |
| `residence_class_en` | varchar(100) | Residence Class En · 可空 |
| `residence_department_ar` | varchar(255) | Residence Department Ar · 可空 |
| `residence_department_en` | varchar(255) | Residence Department En · 可空 |
| `contact_work_phone` | varchar(32) | Contact Work Phone · 可空 |
| `contact_home_phone` | varchar(32) | Contact Home Phone · 可空 |
| `contact_mobile_no` | varchar(32) | Contact Mobile No · 可空 |
| `contact_emirate_en` | varchar(85) | Contact Emirate En · 可空 |
| `contact_emirate_ar` | varchar(85) | Contact Emirate Ar · 可空 |
| `contact_city_en` | varchar(85) | Contact City En · 可空 |
| `contact_city_ar` | varchar(85) | Contact City Ar · 可空 |
| `contact_area_en` | varchar(85) | Contact Area En · 可空 |
| `contact_area_ar` | varchar(85) | Contact Area Ar · 可空 |
| `contact_po_box` | varchar(20) | Contact Po Box · 可空 |
| `contact_building` | varchar(85) | Contact Building · 可空 |
| `contact_flat_no` | varchar(32) | Contact Flat No · 可空 |
| `source` | varchar(50) | Source · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `idx_entity_id`:entity_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
