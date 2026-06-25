---
id: tbl_member_tm_operator
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
- operator-security
- tm_operator
subdomain: operator-security
module: null
sensitivity: restricted
name: 操作员信息表(tm_operator)
aliases:
- tm_operator
related_services:
- svc_member
related_scenarios: []
---

# 操作员信息表(tm_operator)

## 用途
操作员信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `OPERATOR_ID` | varchar(32) | PK / NOT NULL | 操作员编号 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `NICKNAME` | varchar(128) |  | 昵称 |
| `OPERATOR_TYPE` | decimal(8) | NOT NULL | 操作员类型(1个人 2企业) |
| `IS_DEFAULT` | decimal(8) | NOT NULL | 是否为默认操作员(0 否 1是) |
| `STATUS` | decimal(8) | NOT NULL | 状态(0未激活 1正常  3注销) |
| `ACTIVE_TIME` | timestamp |  | 激活时间 |
| `LOCK_STATUS` | decimal(8) | NOT NULL | 锁定状态(0未锁定 1已锁定) |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注 |
| `SECURITY_FLAG` | decimal(8) |  | 安全等级标记 0：默认无  1：数字证书 |
| `PASSWORD` | varchar(64) |  | 登录密码 |
| `GESTURE_PWD` | varchar(64) |  | 手势密码 |
| `FACE_MARK_URL` | varchar(256) |  | 会员头像URL |

## 主键 / 索引
- 主键:(`OPERATOR_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
