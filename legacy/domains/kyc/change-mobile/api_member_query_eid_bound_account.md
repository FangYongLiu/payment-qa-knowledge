---
id: api_member_query_eid_bound_account
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:2654d3b2-24d5-481b-926b-96f41f946ae8
tags:
- dubbo
- member
- eid
subdomain: change-mobile
module: member-facade
sensitivity: normal
name: 查询 EID 绑定会员账号接口 (queryEidBoundAccount)
aliases:
- queryEidBoundAccount
related_services: []
related_tables: []
related_scenarios:
- kyc-change-mobile-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
通过 EID 编号查询该 EID 已绑定的会员账号列表，用于 KYC 换绑手机号流程中展示用户在当前证件下持有的多个钱包账号信息（手机掩码、Ticket、memberId、锁定状态、余额），供选择目标账号。

## 路径/方法
- Dubbo 接口：`com.uaepay.member.service.facade.IMemberFacade#queryEidBoundAccount`

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| eidNum | String | Y | P12365 | Eid number ticket |

## 出参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| memberAccountList | List<MemberAccount> | Y | | 绑定账号列表 |
| --mobileMask | String | Y | +971-23*****80 | Mobile mask |
| --mobileTicket | String | Y | P4100385 | Mobile Ticket |
| --memberId | String | Y | 100000436197 | Member ID |
| --isLock | String | Y | Y | Member is locked |
| --balance | BigDecimal | Y | 100.00 | Basic account balance |

## 错误码
原文未列出。

## 测试校验点
- 输入有效 `eidNum`，返回该 EID 下所有已绑定的会员账号列表。
- `mobileMask` 为脱敏格式（如 `+971-23*****80`）。
- `mobileTicket` 为手机 ticket 而非明文手机号。
- `isLock=Y` 时表示账号被锁定，需在换绑流程中正确识别。
- `balance` 字段返回基础账户余额（BigDecimal），用于用户选择账号时参考。
- 返回的 `memberId` 可用于后续 `changeMobileAndRefreshKyc` 中作为 `originalMemberId` 或 `newMemberId`。
