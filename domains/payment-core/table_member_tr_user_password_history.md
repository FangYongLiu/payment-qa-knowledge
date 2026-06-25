---
id: tbl_member_tr_user_password_history
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
- password-security
- tr_user_password_history
subdomain: password-security
module: null
sensitivity: sensitive
name: User password history(tr_user_password_history)
aliases:
- tr_user_password_history
related_services:
- svc_member
related_scenarios: []
---

# User password history(tr_user_password_history)

## 用途
User password history。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | ID |
| `member_id` | varchar(20) | NOT NULL | Member id |
| `operator_id` | varchar(32) | NOT NULL | Operator id |
| `password_type` | varchar(25) |  | Password type |
| `password` | varchar(80) |  | Password |
| `effect_time` | timestamp |  | Effect time |
| `expiry_time` | timestamp |  | Expiry time |
| `version` | int | 默认 1 | Version |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
