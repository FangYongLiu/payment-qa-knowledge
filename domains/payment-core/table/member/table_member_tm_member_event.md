---
id: tbl_member_tm_member_event
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
- tm_member_event
subdomain: member-profile
module: null
sensitivity: normal
name: member event(tm_member_event)
aliases:
- tm_member_event
related_services:
- svc_member
related_scenarios: []
---

# member event(tm_member_event)

## 用途
member event。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK / NOT NULL | ID |
| `member_id` | varchar(18) | NOT NULL | Member ID that triggered the event |
| `previous_identity` | varchar(64) |  | The identity that triggers the event to modify the phone number |
| `previous_eid` | varchar(18) |  | The eid number corresponding to the original phone number |
| `relation_mid` | varchar(18) |  | The member ID that triggers the event |
| `event_type` | varchar(16) | NOT NULL | ChangeMobile,UpdateUid,Bind,Unbind,Reactive,Cancel |
| `platform` | varchar(32) | NOT NULL | Modify entrance |
| `operator_name` | varchar(64) |  | operator |
| `attachment` | varchar(64) |  | The proof materials |
| `memo` | varchar(255) |  | memo |
| `create_time` | timestamp | NOT NULL | create time |
| `update_time` | timestamp | NOT NULL | update time |

## 主键 / 索引
- 主键:(`event_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
