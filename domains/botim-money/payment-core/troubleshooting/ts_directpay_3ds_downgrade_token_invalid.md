---
id: ts_directpay_3ds_downgrade_token_invalid
object_type: Troubleshooting
name: DirectPay 3DS 降级导致 CardToken 代扣失败
aliases:
- 3DS降级
- CardToken无法代扣
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/702709784 + wiki:70f3c536-29f9-4b13-84f9-fdd88653b2d6
tags:
- DirectPay
- 3DS降级
- CardToken
- 卡激活
related_services:
- svc_payment
- svc_member
related_tables:
- tbl_member_tr_bank_card_token
related_logs: []
related_failures: []
---

# DirectPay 3DS 降级导致 CardToken 代扣失败

## 症状

- 商户用 Direct Pay（直连支付）完成首次支付，PayBy 支付成功后通过 notify 把 `CardToken` 回传给商户。
- 商户下次用该 `CardToken` 发起代扣（后续支付）时失败，无法完成扣款。

## 背景术语（卡状态）

- **激活**：已激活的卡可以用卡 id 查询出卡信息；卡未激活时 `CardToken` 无法用于后续代扣。
- **认证**：用于风控判断风险。未认证卡可走 3DS 认证（认证时需提供 cvv）。

PayBy 三种核心支付场景定义（背景，见 [[scn_online_business_direct_pay]] / [[scn_online_business_auto_debit]]）：
- **Direct Pay**：直连支付，支付成功存卡并返回 `CardToken`，后续凭 token 继续支付。
- **PAYANDSIGN**：支付并签约，用户完成支付即认可代扣协议，PayBy 生成并生效协议。
- **AUTODEBIT**：授权支付，用已生效的代扣协议号扣款。

## 关联关系

- **涉及服务 / 表**：[[svc_payment]]、[[svc_member]] / [[tbl_member_tr_bank_card_token]]（= `related_services` / `related_tables`）
- **相关场景**：循环（tokenized）支付测试见 [[scn_payment_core_mit_cit_mpgs]]；单笔直连见 [[scn_online_business_direct_pay]]

## 可能根因

- 首次 Direct Pay 支付走 3DS 认证时被**降级**（3DS 降级）。
- 当前策略：3DS 降级后**不会**把卡状态更新为「激活」。
- 卡未处于「激活」状态时，`CardToken` 无法用于后续代扣，故代扣失败。

## 排查步骤（DB / Kibana）

1. 根据商户传入的 `CardToken` 定位对应卡记录（[[tbl_member_tr_bank_card_token]]），确认卡是否处于「激活」状态。
2. 查首次 Direct Pay 支付的 3DS 认证流水，确认该笔支付是否发生 3DS 降级。
3. 若卡未激活 + 首次支付存在 3DS 降级记录，即可确认命中本问题。
4. 复核当前 Direct Pay 首次支付链路，确认降级分支未触发卡激活逻辑。

## 处理 / 规避

解决方案（讨论中，待最终结论 — 待补）：
1. 支付成功即更新卡状态为「激活」。
2. 支付成功且**非** 3DS 降级时，更新卡认证状态为「已认证」。
3. 针对特约商户的 motoPay：包装新接口，独立给特约商户授权，不绑卡，直接 moto 扣款。
