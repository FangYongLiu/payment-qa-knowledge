---
id: tbl_member_tr_login_name
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
- identity
- tr_login_name
subdomain: identity
module: null
sensitivity: normal
name: 操作员登录名信息表(tr_login_name)
aliases:
- tr_login_name
related_services:
- svc_member
related_scenarios: []
---

# 操作员登录名信息表(tr_login_name)

## 用途
操作员登录名信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `LOGIN_ID` | decimal(28) | PK / NOT NULL | 登录ID |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `OPERATOR_ID` | varchar(32) | NOT NULL | 操作员编号 |
| `LOGIN_NAME` | varchar(128) | NOT NULL | 登录名 |
| `SOURCE_TYPE` | decimal(8) |  | 来源类型 |
| `LOGIN_NAME_TYPE` | decimal(8) | NOT NULL | 登录名类型(0通行证 1邮箱 2手机) |
| `UUID` | varchar(50) |  | 唯一编号 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`LOGIN_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
