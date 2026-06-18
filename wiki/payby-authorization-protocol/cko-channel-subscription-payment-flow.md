---
title: CKO渠道订阅支付流程
domain: payby-authorization-protocol
kind: wiki_page
slug: cko-channel-subscription-payment-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:bea17c38-8186-48b8-af81-72e06ea7ec56
tags: []
---

# CKO渠道订阅支付流程

本页描述 CKO 渠道下订阅支付的端到端时序，覆盖用户确认支付时的 preferSign 查询与协议匹配、frictionless 3DS 处理，以及验证支付时的卡信息保存与下单确认。

## 参与方

- User：用户
- cgs->cashierii：收银台服务
- grc：协议/规则中心
- member：会员
- authpay：授权支付
- trade：交易
- cmf：卡信息管理
- checkout：CKO 渠道侧

## 阶段一：Confirm card payment（确认支付）

用户在收银台发起 `Confirm card payment`，cashierii 先查询授权支付的 preferSign 标记，再依据结果决定是否走签约协议匹配与 frictionless 3DS。

### preferSign 查询

- 1.1 `Query auth pay perferSign`：cashierii → authpay
- 1.2 `Authorize result (perferSign)`：authpay 返回授权结果与 preferSign

### preferSign=Y 分支：协议匹配与 frictionless

当 `preferSign=Y` 时执行：

- 1.3 `Query sign protocol list`：cashierii → grc 查询已签约协议列表
- 1.4 `Signed protocols`：grc 返回已签协议
- 1.5 `Preroute for card payment channel with signed protocols`：cashierii → checkout，携带已签协议进行卡渠道预路由
- 1.6 `Protocol whether available (frictionless)`：checkout 返回协议是否可用（frictionless 判定）

### Frictionless 支付事件与 3DS

- 1.7 `Payment event with frictionless`：cashierii → authpay
  - 1.7.1 `Save env infor`：authpay 内部保存环境信息
  - 1.7.2 `3ds`：authpay 回调 cashierii 执行 3DS（frictionless 模式）
- 1.8 `Cache context`：cashierii 内部缓存上下文
- 1.9 `Risk result`：cashierii 向 User 返回风控结果

## 阶段二：Verify card payment（验证支付）

用户发起 `Verify card payment`，cashierii 处理 preferSign / frictionless 参数，并保存卡信息后下单。

- 2.1 `Process preferSign and frictionless args`：cashierii 内部处理参数
- 2.2 `Save card information with preferSign or frictionless`：cashierii → cmf，按 preferSign 或 frictionless 保存卡信息
- 2.3 `Card token id`：cmf 返回卡 token id
- 2.4 `Confirm pay`：cashierii → trade 确认支付
  - 2.4.1 trade → cmf

## 相关

- 时序图详见 [[flow_cko_subscription_payment]]
