---
id: api_member_query_eid_bound_account
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1751384142
tags:
- dubbo
- member
- eid
subdomain: eid
module: member
sensitivity: normal
name: 查询EID绑定手机账户接口
aliases:
- queryEidBoundAccount
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
通过 EID 号查询已绑定的会员账户列表，用于 Change Mobile 等场景下选择需要变更/释放的钱包账户。

## 路径/方法
- 类型：Dubbo API
- 接口：`com.uaepay.member.service.facade.IMemberFacade#queryEidBoundAccount`

## 入参
| Parameter | Data Type | Mandatory | Sample | Description |
|---|---|---|---|---|
| eidNum | String | Y | P12365 | Eid number ticket |

## 出参
| Parameter | Data Type | Mandatory | Sample | Description |
|---|---|---|---|---|
| memberAccountList | List<MemberAccount> | Y | Object | 绑定账户列表 |
| --mobileMask | String | Y | +971-23*****80 | Mobile mask |
| --mobileTicket | String | Y | P4100385 | Mobile Ticket |
| --memberId | String | Y | 100000436197 | Member ID |
| --isLock | String | Y | Y | Member is locked |
| --balance | BigDecimal | Y | 100.00 | Basic account balance |

## 错误码
原文未列出。

## 测试校验点
- 入参 eidNum 必填，传入有效 EID 号能返回该 EID 绑定的所有 MemberAccount 列表。
- 出参 memberAccountList 中每个对象需包含 mobileMask、mobileTicket、memberId、isLock、balance 字段。
- mobileMask 按 `+971-23*****80` 格式脱敏。
- isLock 字段正确反映会员锁定状态（Y/N）。
- balance 返回 Basic account 余额，类型为 BigDecimal。
- 该接口返回结果可作为后续 [[api_member_change_mobile_refresh_kyc]] 中 originalMemberId / newMemberId 的候选数据来源。
