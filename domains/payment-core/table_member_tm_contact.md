---
id: tbl_member_tm_contact
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
- tm_contact
subdomain: member-profile
module: null
sensitivity: restricted
name: 联系人信息(tm_contact)
aliases:
- tm_contact
related_services:
- svc_member
related_scenarios: []
---

# 联系人信息(tm_contact)

## 用途
联系人信息。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CONTACT_ID` | varchar(32) | PK / NOT NULL | 主键 |
| `OBJECT_ID` | varchar(32) | NOT NULL | 联系信息所属对象ID |
| `CONTACT_NAME` | varchar(128) |  | 名称 |
| `CONTACT_TYPE` | decimal(8) | NOT NULL | 联系人类型(0会员联系信息 1其他联系人) |
| `COUNTRY` | varchar(255) |  | 国家,区划码 |
| `PROVINCE` | varchar(255) |  | 省份,区划码 |
| `CITY` | varchar(255) |  | 城市,区划码 |
| `TOWN` | varchar(100) |  | 城镇/区/街 |
| `ADDRESS` | varchar(255) |  | 地址 |
| `POSTCODE` | varchar(6) |  | 邮政编码 |
| `MOBILE` | varchar(40) |  | 手机 |
| `TEL` | varchar(20) |  | 电话 |
| `EMAIL` | varchar(100) |  | 邮箱 |
| `POSITION` | varchar(50) |  | 职位 |
| `DEPT` | varchar(50) |  | 部门 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注信息 |
| `STATUS` | decimal(8) | 默认 1 | 0 无效，1有效 |

## 主键 / 索引
- 主键:(`CONTACT_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
