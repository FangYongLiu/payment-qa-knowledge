---
id: tbl_member_td_member_account_config
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
- account
- td_member_account_config
subdomain: account
module: null
sensitivity: restricted
name: 会员账户配置表(td_member_account_config)
aliases:
- td_member_account_config
related_services:
- svc_member
related_scenarios: []
---

# 会员账户配置表(td_member_account_config)

## 用途
会员账户配置表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | int | PK / NOT NULL | 主键 |
| `ACCOUNT_TYPE` | varchar(30) | NOT NULL | 账户类型 |
| `MAX_ACCOUNT_COUNT` | tinyint |  | 一个会员该类型账户最大数目(负数代表无限制) |
| `STATUS` | tinyint |  | 状态(0不可用;1可用) |
| `SUPPORT_MEMBER_TYPES` | varchar(30) |  | 支持的会员类型，以,分隔 |
| `MEMO` | varchar(255) |  | 备注 |
| `SHARE_BASE_PWD` | tinyint | 默认 0 | 是否共用基本户的支付密码 |
| `ACCOUNT_ATTR` | tinyint | NOT NULL | 账户属性：1:对私、2:对公 |
| `ACCOUNT_SUB_TYPE` | int | NOT NULL | 账户子类型,对应dpm中账户类型 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
