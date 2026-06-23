---
title: Jaywan产品Q&A
domain: ppc-card-business
kind: wiki_page
slug: jaywan-product-qa
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: []
---

# Jaywan产品Q&A

本页汇总 Jaywan 预付卡在虚拟卡、实体卡、交易、通知四个主题下的产品规则澄清与决策记录。相关业务域见 [[domain_jaywan_prepaid_card]]，整体方案见 [[jaywan-prepaid-card-overview]]，与供应商侧的澄清见 [[jaywan-vendor-qa]]。

## 虚拟卡

### 申请虚拟卡
- 客户前置条件：已完成 Eid kyc、已设置 payment password、已通过 identification（payment password 或 biometric）；前端需补齐相关导航。
- 未完成 kyc 的 VIP：Phase 1 不支持。
- 风控限制：同一 eid 同一时刻仅允许一张卡，无其他限制。
- 卡号是否落库：是，会保存。
- CustomerName / CustomerMiddleName / CustomerSurName 规则：会员系统仅有 full name 与 family name（非必填），具体拆分规则以 PRD 为准。
- 电话字段规则：
  - `TelephoneMasterCountryCode` 示例：`971`、`86`
  - `TelephoneMasterPhoneCode = left(phone number, 3)`
  - `TelephoneMasterPhone` 取剩余部分
- `ProductNumber`、`SubProductNumber` 配置：TODO（参见 gppc-OP-Env Configuration）。

### 关卡 & 换卡
- Dgpay 不提供 replace virtual card API。处理方式：调用 close API 后再调用 apply API 完成换卡；或等待新的 replace API 上线。**不能**因此移除换卡功能。

### 其他
- 虚拟卡生命周期已对齐（详见 gppc-SD-Jaywan Virtual Card）。

## 实体卡

### 配送追踪
- 物流商对接由 Dgpay 完成，非 mBank/Botim 侧。
- 状态映射规则：TODO。

### 卡激活
- 需要 identification（payment password 或 biometric）。
- 激活前需先完成 PIN set。

### 其他
- 实体卡生命周期已对齐（详见 gppc-SD-Jaywan Physical Card）。

## 交易

### Balance Inquiry
- 若余额不足以支付手续费，是否返回余额：TODO。
- 若客户余额足够支付手续费：在扣费后返回余额。

## 通知

- SMS / BOTIM 通知的具体规范：TODO，参考 MasterCard Prepaid Card 的 ppc-Notifications。

---

相关：交易/清算/对账类的设计见 [[jaywan-clearing-settlement-design]]；阶段范围与排期见 [[jaywan-system-design-phases]]；与 Dgpay 的接口集成见 [[jaywan-dgpay-integration-guide]]。
