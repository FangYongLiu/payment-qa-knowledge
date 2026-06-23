---
id: ts_directpay_3ds_downgrade_token_invalid
object_type: Troubleshooting
domain: payby-authorization-protocol
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/702709784
tags:
- DirectPay
- 3DS降级
- CardToken
- 卡激活
subdomain: null
module: null
sensitivity: normal
name: DirectPay 3DS降级导致CardToken代扣失败排查
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_directpay_first_and_subsequent
related_logs: []
related_requirements: []
related_failures: []
---

## 症状
- 商户使用 Direct Pay 完成首次支付，PayBy 通过 notify 返回 CardToken 给商户。
- 商户下次使用该 CardToken 发起代扣时失败，无法完成扣款。

## 可能根因
- 首次 Direct Pay 支付走 3DS 认证时被降级(3ds 降级)。
- 当前策略：3DS 降级后不会更新卡状态为「激活」。
- 卡未处于「激活」状态时，CardToken 无法用于后续代扣。

相关定义：
- 激活：已激活的卡可以用卡 id 查询出卡信息。
- 认证：未认证卡可以走 3ds 认证(认证时需提供 cvv)，用于风控判断风险。

## 排查步骤(DB/Kibana)
1. 根据商户传入的 CardToken 定位对应的卡记录，确认卡是否处于「激活」状态。
2. 查看首次 Direct Pay 支付的 3DS 认证流水，确认该笔支付是否发生 3DS 降级。
3. 若卡未激活且首次支付存在 3DS 降级记录，即可确认命中本问题。
4. 复核当前 Direct Pay 首次支付链路，确认降级分支未触发卡激活逻辑。

## 处理
解决方案(讨论中)：
1. 支付成功，更新卡状态为「激活」。
2. 支付成功且非 3DS 降级，更新卡的认证状态为「已认证」。
3. 特约商户 motoPay 包装新接口，独立给特约商户授权，不绑卡，直接 moto 扣款。
