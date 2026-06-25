---
id: tbl_member_tr_company_member
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- member-profile
- tr_company_member
subdomain: member-profile
module: null
sensitivity: normal
name: 企业会员信息表(tr_company_member)
aliases:
- tr_company_member
related_services:
- svc_member
related_scenarios: []
---

# 企业会员信息表(tr_company_member)

## 用途
企业会员信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `MEMBER_ID` | varchar(32) | PK / NOT NULL | 会员ID |
| `INDUSTRY` | char(10) |  | 行业类型 |
| `LICENSE_NO` | varchar(128) |  | 商户营业执照 |
| `LICENSE_EXPIRE_DATE` | timestamp |  | 企业营业执照失效时间 |
| `COMPANY_NO` | varchar(50) |  | 企业编号 |
| `LEGAL_PERSON` | varchar(100) |  | 法人代表 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `COMPANY_NAME` | varchar(256) |  | 企业名称 |
| `ADDRESS` | varchar(256) |  | 企业地址 |
| `BUSINESS_SCOPE` | varchar(1024) |  | 营业范围 |
| `TELEPHONE` | varchar(32) |  | 联系电话 |
| `ORGANIZATION_NO` | varchar(128) |  | 组织机构代码 |
| `LEGAL_PERSON_PHONE` | varchar(40) |  | 法人手机号码 |
| `SOCIAL_CREDIT_NO` | varchar(64) |  | 社会信用代码 |

## 主键 / 索引
- 主键:(`MEMBER_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
