---
id: tbl_member_tm_pwd_wrong_input
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
- password-security
- tm_pwd_wrong_input
subdomain: password-security
module: null
sensitivity: normal
name: 密码错误输入记录(tm_pwd_wrong_input)
aliases:
- tm_pwd_wrong_input
related_services:
- svc_member
related_scenarios: []
---

# 密码错误输入记录(tm_pwd_wrong_input)

## 用途
密码错误输入记录。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(28) | PK / NOT NULL | 主键 |
| `SOURCE_ID` | varchar(100) |  | 应用标记 |
| `USER_IP` | varchar(50) |  | 用户IP |
| `OPERATOR_ID` | varchar(32) | NOT NULL | 操作员ID |
| `ACCOUNT_ID` | varchar(50) |  | 账号ID |
| `FLAG` | decimal(8) | NOT NULL | 所属标志（0登录密码，1支付密码） |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `MEMO` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
