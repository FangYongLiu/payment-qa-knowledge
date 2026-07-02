---
id: tbl_member_tm_member_identity_lock
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
- tm_member_identity_lock
subdomain: identity
module: null
sensitivity: normal
name: 会员标识锁定表(tm_member_identity_lock)
aliases:
- tm_member_identity_lock
related_services:
- svc_member
related_scenarios: []
---

# 会员标识锁定表(tm_member_identity_lock)

## 用途
会员标识锁定表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(12) | PK | 主键id |
| `member_id` | varchar(32) |  | 会员id |
| `partner_id` | varchar(32) |  | 平台方 |
| `status` | tinyint(2) |  | 状态1:锁定；0未锁定 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp |  | 修改时间 |
| `unlock_time` | timestamp | NOT NULL | 解锁时间 |
| `memo` | varchar(255) |  |  |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
