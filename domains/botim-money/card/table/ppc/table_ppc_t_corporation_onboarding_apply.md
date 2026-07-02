---
id: tbl_ppc_t_corporation_onboarding_apply
object_type: Table
name: Corporation Onboarding Apply (t_corporation_onboarding_apply)
aliases: [t_corporation_onboarding_apply, ppc.t_corporation_onboarding_apply]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Corporation Onboarding Apply (t_corporation_onboarding_apply)

## 用途
物理表 `ppc.t_corporation_onboarding_apply`,主键 `onboarding_apply_no`。Corporation Onboarding Apply。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `onboarding_apply_no` | bigint | Onboarding Apply No |
| `request_no` | varchar(40) | Request No |
| `card_type` | char(2) | Card Type, MC=Multi-Currency, PR=Payroll |
| `corporation_id` | varchar(50) | Corporation ID |
| `eid_hash` | varchar(68) | Id hash, separate by prefix, PP=Passport, default is EID |
| `eid` | varchar(32) | EID Ticket: UES Ticket |
| `dob` | date | Date of Birth · 可空 |
| `virtual_card_id` | bigint | Related Virtual Card ID · 可空 |
| `status` | char | Status: I=Init, S=Success, F=Fail, SR=Success Related |
| `related` | char | Related: Y=Related, N=No Relate |
| `fail_code` | varchar(50) | Fail Code · 可空 |
| `fail_message` | varchar(200) | Fail Message · 可空 |
| `trx_ref_no` | varchar(32) | Trx Ref No · 可空 |
| `batch_no` | varchar(20) | Batch No · 可空 |
| `extension` | varchar(500) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`onboarding_apply_no`
- `idx_eid_hash`:eid_hash
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
