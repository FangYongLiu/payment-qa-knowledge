---
id: tbl_member_tm_member_grade
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
- tm_member_grade
subdomain: member-profile
module: null
sensitivity: normal
name: 会员等级表(tm_member_grade)
aliases:
- tm_member_grade
related_services:
- svc_member
related_scenarios: []
---

# 会员等级表(tm_member_grade)

## 用途
会员等级表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `GRADE_ID` | varchar(50) | PK / NOT NULL / 默认 '' | 主键 |
| `MEMBER_ID` | varchar(32) |  | 会员编号 |
| `IDENTITY` | varchar(50) | NOT NULL | 会员标识（uid，手机，memberId等） |
| `STATUS` | tinyint(8) | NOT NULL | -1：已失效，0：等级未绑定，1：等级已绑定会员 |
| `BIND_TYPE` | tinyint(8) | NOT NULL | 0：UID，1:邮箱，2:手机，3:会员编号，4:其他 |
| `PARTNER_ID` | varchar(50) |  | 平台ID |
| `SOURCE` | varchar(50) |  | VIP来源 |
| `OWNER_ID` | varchar(255) |  | 所属平台 |
| `MEMBER_GRADE` | varchar(30) |  | 会员等级 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp |  | 修改时间 |
| `MEMO` | varchar(255) |  | 备注 |
| `OPERATOR` | varchar(125) |  | 操作人 |

## 主键 / 索引
- 主键:(`GRADE_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
