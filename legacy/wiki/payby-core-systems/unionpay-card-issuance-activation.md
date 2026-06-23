---
title: UnionPay开卡与激活流程
domain: payby-core-systems
kind: wiki_page
slug: unionpay-card-issuance-activation
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268580390
tags: []
---

# UnionPay开卡与激活流程

本页描述 UnionPay 银联卡的开卡（系统侧无感知触发）与激活（用户侧主动操作）两个阶段的端到端流程，以及相关注意事项。具体应用场景见 [[unionpay-usage-scenarios]]。

## 开卡流程

开卡由 KYC 完成事件触发，全程对用户无感知。详见 [[flow_unionpay_card_issuance]]。

- 触发条件：用户完成 KYC。
- 链路：`escrow` 系统在 KYC 完成后向 `upic` 应用推送通知 → `upic` 收到通知后调用银联接口为用户开通银联卡。
- 落库：开卡成功后记录在 `upic.t_upi_card`，状态为 `OS`。
- 失败场景：正常情况下不会失败，仅在**网络异常**时可能失败。
- 用户感知：**无声息**，用户无感知。

## 激活流程

出于合规要求，用户在实际使用 UnionPay 功能前必须先完成激活。详见 [[flow_unionpay_card_activation]]。

- 激活页面元素：
  - 用户需勾选**同意协议**的选框
  - **激活**按钮
- 操作结果：点击激活按钮后即完成激活，跳转进入 UnionPay 页面。

## 状态与角色

- KYC 状态决定能否开卡（未 KYC 不会触发开卡）。
- 激活状态决定能否使用 UnionPay 各类支付/付款码功能。
- 三类用户分层：未 KYC 用户 / 已 KYC 未激活用户 / 已激活用户，在不同入口下的行为差异参见 [[unionpay-usage-scenarios]]。

## 注意事项

- **开卡无感知**：用户不会感知到开卡过程，但激活是用户可见流程，必须合规执行。
- **upic 扣款接口**是所有 UnionPay 支付场景资金落地的关键接口（NFC 刷卡、付款码被扫、扫商户码支付均最终由银联回调该接口扣款）。
- 外币支付场景下，用户看到的是基于本地汇率的预估 AED 金额，最终实际扣款金额可能与收银台展示存在偏差，详见 [[unionpay-usage-scenarios]]。
