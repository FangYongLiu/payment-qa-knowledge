---
id: tbl_member_tr_deduct_channel
object_type: Table
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- member
- 代扣
- 签约
subdomain: null
module: member
sensitivity: normal
name: 代扣渠道表 tr_deduct_channel
aliases: []
related_services: []
related_tables:
- tbl_member_tr_bank_card_token
- tbl_deduct_t_deduct_protocol
- tbl_protocol_t_contract_sign_info
related_scenarios:
- scn_cko_subscription_test_cards
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 member 库，记录代扣渠道信息。在独立绑卡（wallet→card，固定走 CKO121）签约成功后新增对应记录，作为后续代扣 / 订阅支付可用渠道的判定依据之一。

## 关键列
原文未列明本表具体字段，仅说明：独立绑卡签约成功后会新增记录到本表。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 独立绑卡（wallet→card，渠道 CKO121）签约成功后，校验本表是否新增对应记录。
- 与 `tr_bank_card_token`（核心签约 token，channel=签约渠道、token=加密协议号、status=Y/N）联合校验，确认卡的签约状态一致。
- 数据校验维度（来自 3.6）：银行卡 / 协议维度需同时校验 tr_bank_account、tr_bank_card_token（是否新增、channel、协议号、状态）、tr_deduct_channel。
- 独立绑卡场景下不受支付鉴权 preferSign 配置影响（固定 CKO121），但本表新增依赖签约成功结果。
