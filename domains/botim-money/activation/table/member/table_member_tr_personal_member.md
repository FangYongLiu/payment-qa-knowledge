---
id: tbl_member_tr_personal_member
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
- member-profile
- tr_personal_member
subdomain: member-profile
module: null
sensitivity: restricted
name: 个人会员信息表(tr_personal_member)
aliases:
- tr_personal_member
related_services:
- svc_member
related_scenarios: []
---

# 个人会员信息表(tr_personal_member)

## 用途
个人会员信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `MEMBER_ID` | varchar(32) | PK / NOT NULL | 会员ID |
| `DEFAULT_LOGIN_NAME` | varchar(50) |  | 默认登录名 |
| `TRUE_NAME` | varchar(110) |  | 真实姓名 |
| `CERT_TYPE` | decimal(8) |  | 证件类型 |
| `ID_NO` | varchar(50) |  | 证件号 |
| `GENDER` | decimal(8) |  | 性别(0保密 1男 2女) |
| `BIRTHDAY` | char(8) |  | 生日 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注信息 |
| `WECHAT_INFO` | varchar(1024) |  | 用户绑定的微信信息 |
| `ADDRESS` | varchar(512) |  | 会员地址信息 |
| `COUNTRY` | varchar(64) |  | 国家 |
| `additional_info` | varchar(1024) |  | 会员额外信息，JSON格式 |
| `classification` | varchar(1024) |  | 会员分类信息，JSON格式 |

## 主键 / 索引
- 主键:(`MEMBER_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
