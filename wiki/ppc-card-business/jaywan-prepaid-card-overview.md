---
title: Jaywan预付卡产品总览
domain: ppc-card-business
kind: wiki_page
slug: jaywan-prepaid-card-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan预付卡产品总览

本页汇总 Jaywan 预付卡（与 Dgpay/Dgpays 集成、由 mBank 发卡）项目的整体背景、参考资料、UI 设计入口与产品范围划分，作为业务域 `ppc-card-business` 下的索引页。

## 产品定位

- Jaywan 是基于 Dgpay (Dgpays) 作为 Vendor 的预付卡产品，包含虚拟卡与实体卡两种形态。
- 发卡方为 mBank，Botim 负责钱包侧业务、对账（reconciliation）等运营活动；mBank 负责与 scheme 的清结算（settlement）。
- 余额由 Dgpays / Botim 侧持有的方案存在差异：当前方向为 Dgpays 不维护余额，钱包侧无需做 balance sync。

## 参考文档

- Business Requirements Document
- Queries_Jaywan_mBank_Botim
- PRD（来源 Amir）
- Dgpays API Integration Document（多份）
- Notifications 规范文档（SharePoint）

## UI 设计

- 3.0.0 UI（Jaywan-Prepaid-Card）：Figma `node-id=4-2`
- 4.0.0 UI（My Cards）：Figma `node-id=191-9659`

## 范围划分

项目按阶段与主题分为以下范围，对应详细设计页：

- Phase 1：覆盖优先级 0/1/2 的用例，包含基础能力、虚拟卡、实体卡、交易主流程 → [[jaywan-phase1-system-design]]
- Clearing & Settlement：清算文件处理、结算文件生成、对账规则对齐 → [[jaywan-clearing-settlement-design]]
- Phase 2：Replace Card、Close Card、Manual Release、ChargeFee、Pending Transaction Chasing 等 → [[jaywan-phase2-system-design]]

完整用例与 Vendor / Institution API 映射见 [[jaywan-use-case-list]]；端到端业务流程见 [[flow_jaywan_card_lifecycle]]。

## 关键 API 与能力一览

- Common：`GetToken`、Institution 侧 `get-token`
- Virtual Card：`CreatePrepaidDigitalCard`、`GetPrepaidCards`（含 error recovery）、`GetPrepaidCardInfo`、`UpdatePrepaidCardStatus`、`PrepaidCardPinOperation`、`UpdateMobilePhoneNumber`
- Physical Card：`CreatePrepaidEmbossData`、`ActivatePrepaidCard`、`notify-courier-process`
- Transaction（Institution API）：`provision`、`reversal`、`balance-inquiry`、`declined-transaction`
- Bank Portal：`update-prepaid-card-status`

## 关键产品决策

- 申请前置条件：Eid KYC、已设置支付密码、通过身份核验（支付密码或生物识别）；Phase 1 不支持未 KYC 的 VIP。
- 风控限制：同一 Eid 同时仅允许一张卡；无其他限制。
- 卡号需在我方持久化保存。
- Replace Card：Dgpay 暂无虚拟卡 replace API，采用「先 close 再 apply」方式实现；或等待 Dgpay 新接口。
- Courier 集成由 Dgpay 完成。
- 余额管理：Dgpays 不维护余额，钱包侧无需 balance sync。
- KYC：CBUAE 要求 banking-as-a-service 必须具备 KYC/KYCC，需向 Dgpay/mBank 传递 KYC 信息。
- Chargeback：由 Botim 发起表单给 mBank，mBank 通过 CBUAE 门户提交。

详细 Q&A 见 [[jaywan-product-qa]] 与 [[jaywan-vendor-qa]]。

## 待确认事项（TODO）

- `ProductNumber` / `SubProductNumber` 配置（gppc-OP-Env Configuration）
- Courier 状态映射（`CardProcessStatusID`、`CardProcessSubStatusID` 枚举）
- Balance Inquiry 在余额不足以支付手续费场景下是否返回余额
- SMS / BOTIM 通知规范（参考 MasterCard Prepaid Card 的 ppc-Notifications）
- Card Status Update：Institution 响应失败时 Dgpay 侧状态是否回滚
