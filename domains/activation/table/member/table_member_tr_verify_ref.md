---
id: tbl_member_tr_verify_ref
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
- kyc-verify
- tr_verify_ref
subdomain: kyc-verify
module: null
sensitivity: normal
name: 认证关系表(tr_verify_ref)
aliases:
- tr_verify_ref
related_services:
- svc_member
related_scenarios: []
---

# 认证关系表(tr_verify_ref)

## 用途
认证关系表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `VERIFY_ID` | decimal(28) | PK / NOT NULL | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `VERIFY_ENTITY_ID` | decimal(28) |  | 认证实体ID |
| `ENTITY_ID` | decimal(28) |  | 实体关联ID |
| `VERIFIED_TIME` | timestamp |  | 生效时间 |
| `EXPIRE_TIME` | timestamp |  | 失效时间 |
| `buffer_invalid_time` | datetime |  | 缓冲宽限时间 |
| `last_renew_time` | timestamp |  | 最后renew时间 |
| `real_expire_time` | datetime |  | 真实过期时间 |
| `STATUS` | decimal(8) |  | 状态(-1已解绑被删除 0未绑定 1已绑定) |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `PID` | decimal(8) |  | 所属平台类型 |
| `VERIFY_TYPE` | decimal(8) |  | 认证类型 |
| `SOURCE` | varchar(25) |  | 认证来源 |

## 主键 / 索引
- 主键:(`VERIFY_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
