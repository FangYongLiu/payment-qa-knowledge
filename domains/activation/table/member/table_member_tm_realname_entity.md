---
id: tbl_member_tm_realname_entity
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- kyc-verify
- tm_realname_entity
subdomain: kyc-verify
module: null
sensitivity: restricted
name: 会员用户真实姓名信息表(tm_realname_entity)
aliases:
- tm_realname_entity
related_services:
- svc_member
related_scenarios: []
---

# 会员用户真实姓名信息表(tm_realname_entity)

## 用途
会员用户真实姓名信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `entity_id` | decimal(28) | PK / NOT NULL | 主键 |
| `unifiedno` | varchar(110) |  | 用户统一编号 |
| `id_number` | varchar(110) | NOT NULL | 身份证号 |
| `real_name` | varchar(200) | NOT NULL | 真实姓名 |
| `name_arabic` | varchar(200) |  | 用户真实阿拉伯名称 |
| `name_english` | varchar(200) |  | 用户真实英文名称 |
| `family_name_ar` | varchar(150) |  | 阿语姓 |
| `family_name_en` | varchar(150) |  | 英语姓 |
| `nationality` | varchar(200) |  | 国别名称 |
| `nationality_code` | char(3) |  | 国家alpha2 |
| `birthdate` | varchar(100) |  | 用户出生年月 |
| `gender` | varchar(4) |  | 性别 |
| `marital_status` | varchar(4) |  | 婚姻状况 |
| `religion` | varchar(20) |  | 宗教信仰 |
| `card_no` | varchar(55) |  | 卡片号 |
| `birth_country` | char(3) |  | 出生国家 |
| `photo` | varchar(40) |  | 照片 |
| `create_time` | timestamp |  | 建立时间 |
| `update_time` | timestamp |  | 更新时间 |
| `status` | decimal(8) |  | 状态(1-正常,9-已作废) |
| `source` | varchar(25) |  | 实名来源 |
| `effect_time` | timestamp |  | 启用日期 |
| `invalid_time` | timestamp |  | 停用日期 |
| `occupation` | varchar(125) |  | 职位 |
| `employer` | varchar(125) |  | 雇主 |
| `mobile_no` | varchar(25) |  | ICA reserve mobile |
| `issue_place` | varchar(125) |  | 签发地 |
| `issue_date` | date |  | 颁发日期 |
| `industry` | varchar(175) |  | 行业信息 |
| `passport_info` | varchar(755) |  | eid附带护照信息json |
| `extension` | varchar(455) |  | 扩展 |

## 主键 / 索引
- 主键:(`entity_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
