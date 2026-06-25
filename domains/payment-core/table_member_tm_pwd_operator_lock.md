---
id: tbl_member_tm_pwd_operator_lock
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
- tm_pwd_operator_lock
subdomain: password-security
module: null
sensitivity: normal
name: 密码<操作员>锁定统计表(tm_pwd_operator_lock)
aliases:
- tm_pwd_operator_lock
related_services:
- svc_member
related_scenarios: []
---

# 密码<操作员>锁定统计表(tm_pwd_operator_lock)

## 用途
密码<操作员>锁定统计表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(28) | PK / NOT NULL | 主键 |
| `OPERATOR_ID` | varchar(32) | NOT NULL | 操作员ID |
| `ACCOUNT_ID` | varchar(50) |  | 账号ID |
| `COUNT_START_TIME` | timestamp | NOT NULL | 开始统计错误次数的起始时间点 |
| `LOCK_TIME` | timestamp |  | 被锁定时间点(null:未被锁定) |
| `STATUS` | decimal(8) | NOT NULL | 状态（0无效 ，1有效） |
| `FLAG` | decimal(8) | NOT NULL | 所属标志（0登录密码，1支付密码） |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
