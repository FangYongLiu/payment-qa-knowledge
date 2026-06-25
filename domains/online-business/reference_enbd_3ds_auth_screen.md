---
id: reference_enbd_3ds_auth_screen
object_type: Reference
name: ENBD / Liv 3DS 认证页面与认证方式
aliases: [ENBD 3DS, Liv 3DS, out-of-band 3DS, SMS OTP fallback]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki_image
source_ref: wiki_image:6a4051b7 (ENBD/Liv 3DS认证页面说明)
tags: [online-business, acquiring, 3DS, ENBD, Liv, DirectPay]
related_services: [svc_acquireii]
---

# ENBD / Liv 3DS 认证页面与认证方式

> Emirates NBD(Liv)作为发卡行在 Visa 卡交易中触发的 3-D Secure step-up 认证页面。主认证为推送带外授权(out-of-band),SMS OTP 为兜底。QA 测 DirectPay 3DS 真实持卡人验证分支时的发卡行侧行为参考。

## 认证方式总览
- **主认证**:Liv X App 推送通知带外授权(或 App 内 Home 入口授权)。
  - iOS 推送:标题 `Card Payment Authorization`,正文 `An online payment has been initiated with your card. Please review and verify the payment.`
  - 用户在 Liv X App 内审阅并确认交易即完成 3DS 授权。
- **兜底认证**:页面 `Having trouble?` 区块的 `Try SMS OTP`(无法用推送/App 审批时切 SMS OTP)。
- **终止操作**:`Exit`(中止认证)。

## 页面要素(供断言/识别)
- 页脚品牌 `Powered by: Emirates NBD`;卡组织标识 `VISA`;推送横幅显示 `liv` 图标。
- 主标题 `Authorize your transaction`,引导在 `Liv X App` 点推送完成授权。
- 交易详情字段:`Merchant`(如 PAYBY)、`Amount`(如 Dhs. 1.00 AED)、`Card ending`(掩码如 `************3250`)、`Date`。
- 帮助/说明链接:`Need some help?` / `Learn more about authentication`。

## 关联关系
- **涉及服务**:[[svc_acquireii]] 收单(= `related_services`)。
- **触发上下文**:DIRECTPAY 卡支付 3DS 流程,interactionParams 返回 `threeDSecureDom`,见 [[scn_online_business_direct_pay]] / [[reference_acquire_protocol_and_codes]]。

## QA 关注点
- 3DS step-up 的两条路径:推送带外授权(主)与 SMS OTP(兜底);Exit 中止。
- 交易详情字段(商户名/金额/卡尾号掩码)与下单一致;卡尾号脱敏。
