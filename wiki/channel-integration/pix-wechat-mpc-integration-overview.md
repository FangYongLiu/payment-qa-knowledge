---
title: 微信MPC渠道接入总览(pix-RA-2405)
domain: channel-integration
kind: wiki_page
slug: pix-wechat-mpc-integration-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: []
related_services:
  - svc_basis_customer
  - svc_payment
  - svc_pix
  - svc_reconciliation
  - svc_remittance
  - svc_tradeii
---

# 微信MPC渠道接入总览(pix-RA-2405)

本页汇总微信"商户出示码（Merchant Presented Code, MPC）"收单接入的业务背景、参考资料与端到端业务/系统流程脉络，作为该渠道接入相关文档的入口。

## 业务背景

- 场景：Pay in China —— 微信 MPC（Merchant Presented Code，商户出示码 / 扫码支付）。
- 用户从钱包侧扫描微信收款码，按汇率换算后以 AED 支付，资金最终以 CNY 结算给商户。
- 同类产品参考：支付宝（AliPay Plus UPM/MPP）。

## 参考资料

- Online Documents：PRD & API Document
- Git Documents：`http://gitlab.test2pay.com/pay/doc/doc-payment/-/tree/master/pix/1-Requirement/20240415_wechat_mpc`
- Union Pay PRD：`https://docs.google.com/document/d/1HRxbhJK-NfWiS7Tlf9FnzCnvFOmcizSROCr1P6QvKX4/edit#heading=h.v8dnv1he5sjs`
- PRD：Pay in China-Wechat
- UI（Figma）：`https://www.figma.com/design/MNlcK9NG3g3YIDbin5WduI/Scan-to-pay`
- AliPay Documents：`https://docs.alipayplus.com/alipayplus/alipayplus/product_intro_mpp/product_upm_mpp?role=MPP&product=Payment1&version=1.5.2`
- 业务流程介绍：Pay into China - Merchant Presented QR Product Introduction（29th March）

## 整体业务流程

参考《Pay into China - Merchant Presented QR Product Introduction》中描述的 MPC 业务流程：钱包侧扫商户码 → 解析商户信息与汇率 → 确认并支付 → 渠道返回支付结果 → 必要时退款 / 关单 / 推定退款 / 对账。

## 系统流程概览

围绕 MPC 全生命周期，pix 侧涉及以下子流程，每个子流程由独立页面承载详细设计：

- **汇率同步（Rate Sync）**：周期性从 remittance 同步基础汇率，叠加渠道侧 Margin Percent 后形成对客汇率，用于支付金额换算。详见 [[pix-wechat-rate-sync]]。
- **解析码（Scan and parse code）**：MpcFacade.parseCode 调用 vendor 获取商户信息并写入 ES（含汇率信息）。归档于 [[flow_pix_wechat_mpc_payment]]。
- **创建交易并支付（Create trade and pay）**：钱包侧按汇率算出 AED 金额；pix-wechat 侧 MpcFacade.creatTrade 在 vendor 创建订单、生成 cashier trade order 并返回 cashierUrl；通过 process result 处理支付通知、记账、对账落地。详见 [[flow_pix_wechat_mpc_payment]]。
- **查询交易结果（Query trade result）**：实现 dubbo facade，按 pix-SD-MPC 查询本地交易状态。
- **退款（Refund）**：异步发起退款请求并通知 refund bill；退款支付金额计算公式：`Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount`。详见 [[flow_pix_wechat_refund]]。
- **关闭支付（Close Payment）**：实现 vendor api 关闭交易，需注意微信侧关单逻辑。
- **最终支付结果（Final payment result）**：处理 NOTIFY_FINAL_PAYMENT_RESULT；若最终失败，触发退款。
- **查询/推定退款**：QUERY_REFUND_ORDER_INFO 用于退款状态查询；NOTIFY_PRESUPPTIVE_REFUND_SUCCESS 为退款推定 —— 经过多次查询且 10 分钟无结果后执行推定，默认仅推定通知 1 次，一旦推定即按退款成功处理，钱包可通过次日账单获取该推定交易记录。
- **对账（Reconciliation）**：通过专用 api 下载对账文件，pix 借助 ufs 存储并保存 fileTag；reconciliation 服务配置自动对账任务并通过 dubbo api 拉取 fileTag。详见 [[flow_pix_wechat_reconciliation]]。

## 涉及系统与职责

- **pix / pix-wechat**：渠道接入主体，承载 MpcFacade、vendor api 调用、交易/退款/关单/推定/对账文件下载等。
- **wallet（App）**：扫码入口、按汇率计算 AED 应付金额并发起确认。
- **remittance**：提供基础汇率（AED → 本币）的查询能力。
- **basis-customer**：汇率与 Margin 的查询/配置 UI。
- **tradeii / pfs / payment**：保存来自 cmf 的 instOrderNo（关键字 DbtrBankId）并提供变更 api。
- **bill**：账单配置与同步。
- **reconciliation**：自动对账任务调度与配置。

## 关联页面

- 渠道汇率与计费：[[pix-wechat-rate-sync]]
- Vendor API 清单与场景映射：[[pix-wechat-vendor-api-catalog]]
- 接入配置项：[[pix-wechat-configuration]]
- 字段含义与 Q&A：[[pix-wechat-qa-notes]]
- 端到端流程：[[flow_pix_wechat_mpc_payment]] / [[flow_pix_wechat_refund]] / [[flow_pix_wechat_reconciliation]]
