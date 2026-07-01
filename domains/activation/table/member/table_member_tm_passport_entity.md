---
id: tbl_member_tm_passport_entity
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
- tm_passport_entity
subdomain: kyc-verify
module: null
sensitivity: restricted
name: 会员护照信息表(tm_passport_entity)
aliases:
- tm_passport_entity
related_services:
- svc_member
related_scenarios: []
---

# 会员护照信息表(tm_passport_entity)

## 用途
会员护照信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `passport_id` | bigint(35) | PK / NOT NULL | 主键 |
| `passport_type` | varchar(32) |  | 护照类型 |
| `passport_nationality` | varchar(200) |  | 护照国籍 |
| `nationality_code` | char(2) |  | 两位国籍code |
| `passport_country_code` | varchar(20) |  | 国家码 |
| `passport_name` | varchar(200) | NOT NULL | 姓名 |
| `passport_no` | varchar(200) | NOT NULL | 护照编号 |
| `passport_birth_date` | datetime |  | 生日 |
| `passport_gender` | varchar(20) |  | 性别 |
| `passport_address` | varchar(800) |  | 住址地址 |
| `passport_expiry_date` | datetime | NOT NULL | 护照有效期 |
| `issue_date` | datetime |  | 护照颁发日期 |
| `industry` | varchar(85) |  | 行业信息 |
| `status` | varchar(20) | NOT NULL | 状态 |
| `create_time` | timestamp | NOT NULL | 建立时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`passport_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
