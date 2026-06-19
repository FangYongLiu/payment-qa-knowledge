---
id: tbl_dpm_db
object_type: Table
domain: payment-database-reference
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 账户
- 余额
- 会员
subdomain: 会员账户
module: null
sensitivity: normal
name: 会员账户库(dpm)核心表
aliases:
- dpm
related_services: []
related_tables:
- tbl_member_db
- tbl_trade_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
dpm 为会员账户库，记录会员的外部账户、外部账户分户信息及内外部账户的余额变动明细，用于支撑会员账户余额查询与账务核对。

## 关键列
- `t_dpm_outer_account`：会员外部账户信息
- `t_dpm_outer_account_subset`：外部账户分户表
- `t_dpm_outer_account_sub_detail`：外部账户分户账户明细，记录外部账户余额变动明细
- `t_dpm_inner_account_detail`：内部账户余额明细

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 余额变动场景需核对 `t_dpm_outer_account_sub_detail`(外部账户分户账户明细)与 `t_dpm_inner_account_detail`(内部账户余额明细)是否同步生成对应明细。
- 外部账户(`t_dpm_outer_account`)与其分户(`t_dpm_outer_account_subset`)的关联完整性。
- 会员账户相关查询通常需结合 [[tbl_member_db]] 中的会员/账户信息进行联查校验。
