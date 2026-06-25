---
id: tbl_aml_t_member_info
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_member_info
subdomain: aml
module: null
sensitivity: normal
name: kyc人员信息表(t_member_info)
aliases:
- t_member_info
related_services:
- svc_aml
related_scenarios: []
---
# kyc人员信息表(t_member_info)

## 用途
kyc人员信息表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `member_id` | varchar(50) |  | 会员id |
| `identify_number` | varchar(50) |  | 身份证ID |
| `name` | varchar(255) |  | 姓名 |
| `gender` | tinyint(1) |  | 性别 |
| `birth_date` | varchar(100) |  | 出生日期 |
| `country` | varchar(50) |  | 国家 |
| `entity_type` | varchar(30) |  | 实体类型 |
| `receive_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 接收数据时间 |
| `kyc_status` | varchar(10) |  | kyc状态 |
| `kyc_type` | varchar(10) |  | kyc类型 |
| `religion` | varchar(30) |  | 宗教信仰 |
| `marital_status` | tinyint(1) |  | 婚姻状态 |
| `idn_photo_front` | varchar(255) |  | 身份证正面照片 |
| `idn_photo_back` | varchar(255) |  | 身份证反面图片 |
| `live_picture` | varchar(255) |  | 活体照片 |
| `update_file` | varchar(255) |  | 通道返回图片 |
| `country_desc` | varchar(255) | 默认 '' | 国家描述 |
| `address` | varchar(255) | 默认 '' | 地址 |
| `expire_date` | varchar(32) | 默认 '' | 过期时间 |
| `push_type` | varchar(32) | 默认 '' | KYC_FINISH，PASSPORT_FINISH |
| `passport_type` | varchar(32) | 默认 '' | 护照类型 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
