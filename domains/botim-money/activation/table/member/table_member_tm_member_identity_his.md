---
id: tbl_member_tm_member_identity_his
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
- tm_member_identity_his
subdomain: identity
module: null
sensitivity: normal
name: 会员标识历史表(tm_member_identity_his)
aliases:
- tm_member_identity_his
related_services:
- svc_member
related_scenarios: []
---

# 会员标识历史表(tm_member_identity_his)

## 用途
会员标识历史表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK | 主键id |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员编号 |
| `IDENTITY` | varchar(50) | NOT NULL | 会员标识 |
| `STATUS` | tinyint | NOT NULL | 1：有效；0：无效 |
| `IDENTITY_TYPE` | tinyint | NOT NULL | 标识类型（0：uid 1：邮箱 2:手机） |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp |  | 修改时间 |
| `MEMO` | varchar(255) |  | 备注 |
| `PID` | int | NOT NULL / 默认 0 | 平台类型 |
| `operate_type` | varchar(32) |  | 操作类型，解绑：unbind，注销：cancel，换号：change |
| `event_id` | bigint |  | relation member_event id |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
