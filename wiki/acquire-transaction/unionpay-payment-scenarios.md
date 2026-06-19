---
title: UnionPay 支付场景总览
domain: acquire-transaction
kind: wiki_page
slug: unionpay-payment-scenarios
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268580403
tags: []
---

# UnionPay 支付场景总览

UnionPay 在我们体系内支持四种支付场景：HCE 刷卡、扫码付款码、扫码商户码（含外币）、EC 银行卡支付。所有场景的资金扣款最终都通过 upic 应用从用户钱包完成。

## HCE 刷卡

- 用户在 Android 手机开启 NFC 后，可在支持银联支付的 POS 机上刷卡
- 刷卡时银联调用 upic 扣款接口，从用户钱包完成扣款

## 扫码付款码

- 商户终端设备支持银联扫码支付时，可扫描用户的银联付款码完成支付
- 扫码后银联调用 upic 扣款接口，从用户钱包扣款
- 当前情况：阿联酋暂无支持；中国可用

## 扫码商户码

商户生成支持银联支付的二维码后，用户用 Botim App 扫码，进入我们的下单页面。

下单页展示：

- 商户信息
- 金额输入框
- Pay 按钮

### 外币场景

- 金额输入框可能为外币，用户只能输入外币金额
- 页面展示"约等于 AED 金额"，汇率由数据库每日从银联官网同步
- 点击 Pay → 呼起收银台，展示预估的 AED 金额
- 支付校验通过后调用银联支付接口，银联返回真实 AED 金额
- 由于用户流程已结束，实际扣款金额可能与收银台展示金额存在偏差

## EC 模式（银行卡支付）

在支持银联卡支付的商户页面：

1. 用户输入银联卡号、有效期、CVV
2. 银联要求用户输入手机号，系统发送短信验证码
3. 用户输入验证码并验证通过
4. 银联调用 upic 应用，通过钱包余额扣款完成支付

## 相关文档

- upic-银联码
