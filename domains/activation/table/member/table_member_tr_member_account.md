---
id: tbl_member_tr_member_account
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
- tr_member_account
subdomain: account
module: null
sensitivity: normal
name: 会员账户信息表(tr_member_account)
aliases:
- tr_member_account
related_services:
- svc_member
related_scenarios: []
---

# 会员账户信息表(tr_member_account)

## 用途
会员账户信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(28) | PK / NOT NULL | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员编号 |
| `ORIGINAL_REQUEST_NO` | varchar(64) | NOT NULL | 开户接口请求号 |
| `ACCOUNT_TYPE` | varchar(30) |  | 账户类型 |
| `ACCOUNT_ID` | varchar(50) |  | 账户编号 |
| `ACCOUNT_ATTRIBUTE` | decimal(8) | NOT NULL | 账户属性(1:对私 2:对公) |
| `STATUS` | decimal(8) | NOT NULL | 状态(0未激活 1正常 2锁定 3止出 4止入) |
| `ALIAS` | varchar(256) |  | 账户别名 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `CATEGORY` | varchar(64) | 默认 'DPM' | 类别: DPM,CREDIT |
| `TYPE_ID` | varchar(64) |  | 类型id |
| `CURRENCY` | varchar(30) |  | 币种 |
| `OUT_ACCOUNT_TOKEN` | varchar(50) |  | 外部账户Token |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
