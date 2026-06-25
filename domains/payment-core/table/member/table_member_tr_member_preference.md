---
id: tbl_member_tr_member_preference
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
- tr_member_preference
subdomain: member-profile
module: null
sensitivity: normal
name: 用户偏好表(tr_member_preference)
aliases:
- tr_member_preference
related_services:
- svc_member
related_scenarios: []
---

# 用户偏好表(tr_member_preference)

## 用途
用户偏好表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | int(10) | PK | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL / 默认 '' | 会员id |
| `PREFERENCE_TYPE` | varchar(255) | 默认 '' | 偏好类型 |
| `CONTEXT` | varchar(100) | 默认 '' | 偏好内容 |
| `BIZ_ID` | int(10) |  | 业务id |
| `STATUS` | varchar(3) | 默认 '' | 状态（1有效 0无效） |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `MODIFY_TIME` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
