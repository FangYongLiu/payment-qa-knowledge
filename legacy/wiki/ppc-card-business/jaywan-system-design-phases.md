---
title: Jaywan系统设计阶段规划
domain: ppc-card-business
kind: wiki_page
slug: jaywan-system-design-phases
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: []
---

# Jaywan系统设计阶段规划

本页梳理 Jaywan 预付卡项目在 Phase 1、清结算（Clearing & Settlement）以及 Phase 2 的系统设计任务清单，包含每项任务的 Dgpay API、简要说明、优先级、工作量与开发分工。整体业务背景见 [[jaywan-prepaid-card-overview]]，对接细节见 [[jaywan-dgpay-integration-guide]]，所属业务域为 [[domain_jaywan_prepaid_card]]。

## 阶段划分与优先级口径

- **Phase 1**：覆盖优先级 0、1、2 的用例。
- **Clearing & Settlement**：清结算独立成块，单独排期，详见 [[jaywan-clearing-settlement-design]]。
- **Phase 2**：补齐换卡、销卡、手动放行、ChargeFee、长时间未平挂账追踪等能力。
- 优先级数值越小越靠前；同一类用例同时作为 Vendor API 与 Institution API 出现时分别拆分。

## Phase 1 任务清单

### Basic（基础能力）
- **Key Management（90%）**：内部接口取密钥；加解密接口，参考 `gppc-OP-Key Generation` Wiki 的 Encryption Process。优先级 0，1.5d，huihua.ni。
- **Apply vendor token（100%）**：对接 `GetToken`，内部 API 申请与管理 vendor token；旧 token 过期前异步生成新 token；统一封装通用请求过程（token 注入与 pojo 转换）；单测中 mock vendor responder。优先级 0，3d，huihua.ni。
- **Generate institution token（90%）**：实现 Institution `GetToken`，生成与管理 institution token；统一封装通用响应流程（token 校验与 pojo 转换）；单测中 mock vendor requester。优先级 1、2，2d，yu.tang。

### Virtual Card（虚拟卡）
- **Apply virtual card（100%）**：对接 `CreatePrepaidDigitalCard`；CGS API 包含 Summary Query、Init Apply、Apply。优先级 0，3d，yu.tang。
- **Query Card Info（90%）**：对接 `GetPrepaidCards`；CGS API 用于 View Card Detail。优先级 0，0.5d，yu.tang。
- **PIN Set（80%）**：对接 `PrepaidCardPinOperation`；CGS API 用于 Set Card PIN。优先级 0，1d，yu.tang。
- **Lock/Unlock Card（100%）**：对接 `UpdatePrepaidCardStatus`；CGS API 用于 Lock / Unlock Card。优先级 0，0.5d，yu.tang。
- **Apply virtual card - recovery（100%）**：通过 `GetPrepaidCards` 自动从 vendor 错误中恢复。优先级 3，0.5d?，yu.tang。
- **Update Mobile（100%）**：手机号变更时通过 `UpdateMobilePhoneNumber` 同步至 Dgpay。优先级 3，0.5d?，yu.tang。
- **Update status from bank portal（90%）**：实现 Institution `UpdatePrepaidCardStatus`。优先级 3，0.5d?，yu.tang。
- **Apply virtual card with pay（90%）**：CGS API；支持 with pay 与 with physical card；过期已存在的失败申请；可与实体卡一并申请；接收交易结果更新状态并异步申请虚拟卡与实体卡。优先级 3，3d，cong.zhou。

### Physical Card（实体卡）
- **Apply physical card（100%）**：对接 `CreatePrepaidEmbossData`；CGS API 包含 Init Apply、Apply、Tracking；支付费用并申请实体卡。优先级 1，3d，huihua.ni。
- **Activate Physical Card（100%）**：对接 `ActivatePrepaidCard`，CGS API。优先级 1，0.5d，huihua.ni。
- **Delivery tracking（90%）**：实现 Institution `NotifyCourierProcess`。优先级 1、2，0.5d，yu.tang。
- **Apply physical card - recovery**：vendor 错误自动恢复。优先级 3，0.5d?，yu.tang。

### Transaction（交易）
- **Provision（90%）**：实现 Institution `Provision` 报文；集成风控、支付、账单、PNS 等服务；支持 Transaction 与 Refund。优先级 1、2，3d，yu.tang。
- **Balance Inquery（90%）**：实现 Institution `Balance Inquery` 报文；新增余额查询。优先级 1、2，0.5d，yu.tang。
- **Reversal（90%）**：实现 Institution `Reversal` 报文；附加重试流程。优先级 1、2，1d，yu.tang。
- **Declined Transaction（100%）**：实现 Institution `Declined Transactions`；保存被拒交易；按需发送通知。优先级 3，0.5d?，yu.tang。

## Clearing & Settlement 任务清单

设计文档：`gppc-SD-Jaywan Clearing & Settlement`。详细规则见 [[jaywan-clearing-settlement-design]]。

- **Clearing file process frame**：Clearing File 处理框架；与 `Clearing detail process - DECLINE` 一并实现；在已有流程中加入 settlement detail 生成。优先级 0，2d，yu.tang。
- **Clearing detail process - OFFLINE**：OFFLINE 类型清算处理。优先级 1，1d，yu.tang。
- **Clearing detail process - PROVISION, BALANCE_INQUERY**：对应类型的清算处理。优先级 1，2d，yu.tang。
- **Clearing detail process - REVERSAL**：REVERSAL 清算处理；为 single message reversal 增加反向 settlement 更新。优先级 2，3d，yu.tang。
- **Settlement file generation**：在 single messages 流程中加入 settlement detail 生成；产出 Settlement File。优先级 3，2d，yu.tang。
- **Reconciliation**：与 CS 团队对齐对账规则；在已有流程中加入对账数据发送。优先级 4，2d，yu.tang。

## Phase 2 任务清单

- **Replace Card**：组合调用 `UpdatePrepaidCardStatus` + `CreatePrepaidDigitalCard`，CGS API；1d，yu.tang。
- **Close Card**：`UpdatePrepaidCardStatus`，CGS API；附加 close member check；1d?，yu.tang。
- **Manual Release**：人工放行长时间未入账的 dual message。
- **ChargeFee**：Institution API；实现 `ChargeFee` 与 `ChargeFeeCancel`，对应设计 `gppc-SD-Jaywan Transaction`。
- **Pending Transaction Chasing**：Internal Mechanism，挂账交易追踪机制。

## 相关 Q&A

- 产品侧确认见 [[jaywan-product-qa]]。
- 供应商（Dgpay）侧确认见 [[jaywan-vendor-qa]]。
