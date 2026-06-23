---
id: tbl_member_tr_bank_card_token
object_type: Table
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- member
- contract
- token
- CKO
- subscription
subdomain: member
module: bank-card
sensitivity: normal
name: 银行卡签约Token表
aliases:
- tr_bank_card_token
related_services:
- svc_member
---

## 用途
银行卡签约 token 表（核心），位于 `member` 库。存储用户银行卡通过 CKO 签约渠道（CKO102 支付绑卡并签约 / CKO121 独立绑卡）成功后，由 CKO 返回的 `signTransactionId` 加密后落地的 token。后续支付过程中，通过判断该表是否存在有效数据（`status=Y`），来确定该卡是否已签约。已签约卡可在 preferSign=Y 且核身为非 3DS（密码 / 免密）场景下，路由到 CKO111 订阅 / 代扣渠道。

## 关键列
- `channel`：签约渠道，标识该卡通过哪个 CKO 渠道完成签约（如 CKO102 / CKO121）
- `token`：CKO 返回字段 `signTransactionId` 加密后的值，作为该卡的签约凭证（加密协议号）
- `status`：签约状态，`Y` = 有效（视为已签约），`N` = 无效
- 收银台在签约成功后基于绑卡消息（带 `signTransactionId`、`signSource=CKO`）写入本表

## 主键/索引
- 原文未明确说明主键与索引设计

## 校验点(QA 关注)
- **签约落库**：preferSign=Y + is3DS=Y 命中 CKO102（支付绑卡并签约）或走 CKO121 独立绑卡，绑卡 / 支付成功后须校验 `member.tr_bank_card_token` 新增一条记录，且 `channel`、`token`、`status` 三列正确写入
- **token 加密**：落库的 `token` 字段值应为 CKO 返回的 `signTransactionId` 加密后的结果（非明文）
- **status 有效性**：仅 `status=Y` 的行视为该卡已签约；后续 confirmPayInfo 阶段「查询卡签约渠道」依赖该有效行
- **路由联动**：已签约卡（本表存在 status=Y 行）+ preferSign=Y + 核身非 3DS（密码 / 免密）时，路由应命中 CKO111，且收银台 verify 阶段传 `frictionless=Y`
- **不签约场景**：preferSign=N / Null，或 preferSign=Y 但签约渠道不可用降级到 CKO101 时，不应在本表新增有效行
- **失败场景**：使用 `4870 5270 1770 0692`（认证拒绝）、`4544 2491 6767 3670`（渠道返回失败）等异常卡号，绑卡 / 签约失败时不应产生有效记录
- **解绑 / 重签**：解绑后再签约场景，校验旧记录 `status` 变更与新记录写入逻辑
- **关联表一致性**：本表的签约状态应与 `tr_deduct_channel`、`t_deduct_protocol.deduct_protocol_no`、`t_contract_sign_info.sign_contract_no` 在订阅 / 代扣链路上保持一致
