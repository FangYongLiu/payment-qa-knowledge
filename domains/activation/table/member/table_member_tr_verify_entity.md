---
id: tbl_member_tr_verify_entity
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
- tr_verify_entity
subdomain: kyc-verify
module: null
sensitivity: normal
name: 认证实体表(tr_verify_entity)
aliases:
- tr_verify_entity
related_services:
- svc_member
related_scenarios: []
---

# 认证实体表(tr_verify_entity)

## 用途
认证实体表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `VERIFY_ENTITY_ID` | decimal(28) | PK / NOT NULL | 主键 |
| `VERIFY_TYPE` | decimal(8) | NOT NULL | 认证类型(1身份证 , 11 手机 12信箱) |
| `VERIFY_ENTITY` | varchar(110) | NOT NULL | 认证实体 |
| `VERIFY_SUB_TYPE` | decimal(8) |  | 认证子类型 |
| `CHANNEL` | decimal(8) |  | 认证渠道 |
| `STATUS` | decimal(8) |  | 状态(0未认证 1已认证) |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `VERIFY_SUMMARY` | varchar(255) |  | 认证摘要 |
| `TRUE_NAME` | varchar(110) |  | 真实姓名 |
| `ENTITY_ID` | decimal(28) |  | 关联具体实体信息的ID |
| `EFFECT_TIME` | timestamp |  | 认证的启用日期 |
| `INVALID_TIME` | timestamp |  | 认证的过期日期 |

## 主键 / 索引
- 主键:(`VERIFY_ENTITY_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
