---
id: tbl_member_tr_bank_card_token
object_type: Table
domain: authorization-protocol
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:9770c9b6-cd5c-4f9d-ae94-6d4e4b107220
tags:
- 签约
- Token
- CKO
subdomain: member
module: null
sensitivity: normal
name: 银行卡签约Token表
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_cko_standalone_card_binding
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储用户银行卡通过 CKO 签约渠道（如 CKO121）独立绑卡成功后，由 CKO 返回的 `signTransactionId` 加密后落地的 token。后续支付过程中，通过判断该表是否存在有效数据，来确定该卡是否已签约。已签约的卡可走 moto 渠道场景（对应 CKO 签约渠道）。

## 关键列
- token：CKO 返回字段 `signTransactionId` 加密后的值，用于标识该卡的签约凭证

## 主键/索引
- 原文未明确说明主键与索引设计

## 校验点(QA 关注)
- 走 CKO121 独立绑卡场景，绑卡成功后需校验 `member.tr_bank_card_token` 是否落库一条记录
- 落库的 token 字段值应为 CKO 返回的 `signTransactionId` 加密后的结果（非明文）
- 后续支付时，系统应基于该表是否存在有效数据判断卡是否已签约
- 已签约卡参与 moto 渠道场景支付时，路由应能匹配到对应的 CKO 签约渠道（如 CKO111）
- 绑卡失败场景（如使用 `4870 5270 1770 0692` Authentication rejected 卡号）下，不应在该表中产生数据
