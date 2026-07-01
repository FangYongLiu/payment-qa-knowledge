---
id: tbl_member_tm_member_invitation_code
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
- tm_member_invitation_code
subdomain: member-profile
module: null
sensitivity: normal
name: 会员邀请码表(tm_member_invitation_code)
aliases:
- tm_member_invitation_code
related_services:
- svc_member
related_scenarios: []
---

# 会员邀请码表(tm_member_invitation_code)

## 用途
会员邀请码表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK | 主键 |
| `member_id` | varchar(32) |  | 会员id |
| `invitation_code` | varchar(255) | NOT NULL | 邀请码 |
| `status` | varchar(2) | NOT NULL | 状态（是否有效）Y有效N无效 |
| `extension` | varchar(255) |  | 拓展字段 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |
| `invitation_type` | varchar(16) |  | personal个人 company公司 |
| `code_source` | varchar(32) |  | 邀请码来源 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
