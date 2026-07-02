---
id: flow_remittance_pix_mpc
object_type: Flow
name: PIX MPC 商户呈现码扫码支付端到端流程
aliases: [PIX MPC, Merchant Presented Code, pix-RA-2405-STP-Wechat]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/517832723; wiki_image:ef3f6539-9124-400a-b7f2-096dfe2a2761
tags: [PIX, MPC, 扫码支付, wechat]
related_services: [svc_pix, svc_cgs, svc_tradeii]
related_tables: []
related_scenarios: []
---

# PIX MPC 商户呈现码扫码支付端到端流程

## 概述
PIX MPC(Merchant Presented Code,商户呈现码)是 PIX 场景下由商户出示二维码、用户扫码完成的支付方式。整体由 wallet(钱包前端,客户端入口)、[[svc_pix]](CGS API 层)、pix-channel(渠道实现)三方协作完成,分四阶段:扫码解析 → 确认交易信息 → 支付处理 → 展示交易结果。
> 注:wallet 与 pix-channel 服务对象尚未建立(**待补**),正文以纯文字标注,不连边;[[svc_pix]] 属 payment-core,本流程因 wiki 归属标 remittance。

## 步骤(跨系统)

### 1 scan(扫码与解析)
- wallet 调用 [[svc_pix]] `/pix/mpc/v1/get-rules` 获取商户码匹配规则;wallet 可缓存规则至少 2 天,当前支持匹配类型 `PREFIX`。
  - pix → pix-channel(待补)`MpcFacade.getMatchRules`。
- wallet 用规则匹配扫到的 QrCode,命中后调用 [[svc_pix]] `/pix/mpc/v1/parse` 解析:pix 调渠道实现匹配 vendor code,获取商户与交易信息(含费率),返回 code id;wallet 展示商户与交易信息。
  - pix → pix-channel(待补)`MpcFacade.parseCode`。

### 2 confirm trade information(确认交易信息)
- wallet 可选输入支付金额、可选按 rate 计算本币金额。
- wallet 调用 [[svc_pix]] `/pix/mpc/v1/create-trade` 创建交易:返回 `cashierToken`,pix 侧按 rate 配置校验金额。
  - pix → pix-channel(待补)`MpcFacade.parseCode`。

### 3 payment process(支付处理)
- 走 wallet 已有的 cashier 收银台支付流程。
- (RA-2405 微信/Tenpay 子链路)确认交易信息后:wallet → [[svc_cgs]] `/pix/mpc/v1/create-trade` → [[svc_pix]];[[svc_pix]] 作为编排核心:先向 vendor(Tenpay,待补)发起 scan code for payment,再调 [[svc_tradeii]] `CashierTradeFacade#createCashierTrade` 落库收银台交易,逐层返回 wallet 渲染收银台(show cashier);用户在收银台完成后续支付(complete cashier flow)。

### 4 show trade result(展示交易结果)
- 收银台支付成功后 wallet 跳转 MPC 结果页,调用 [[svc_pix]] `/pix/mpc/v1/query-trade` 查询交易信息并展示。

## 关联关系
- **经过的服务(有序)**:wallet(待补)→ [[svc_cgs]] → [[svc_pix]] → pix-channel(待补)/ vendor(待补)→ [[svc_tradeii]](= `related_services`,已建对象部分)
- **关键表**:待补
- **关键场景**:待补
- **配套**:bill 账单配置(Owner: Yongxin Cao)、reconciliation 对账配置(Owner: Yibin Xia)

## Dubbo Facade(pix-channel 实现 `MpcFacade`)
- `MpcFacade.getMatchRules`:被 `/pix/mpc/v1/get-rules` 调用。
- `MpcFacade.parseCode`:被 `/pix/mpc/v1/parse`、`/pix/mpc/v1/create-trade`、`/pix/mpc/v1/query-trade` 调用。

## 校验点
- wallet 对 merchant code rules 的缓存有效期至少 2 天;匹配规则类型支持 `PREFIX`。
- `/pix/mpc/v1/parse` 返回须含 vendor code、商户与交易信息、费率信息及 code id。
- `/pix/mpc/v1/create-trade` 须按费率配置校验金额并返回 `cashierToken`。
- 支付成功后须从 cashier 结果页跳转 MPC 结果页,并经 `/pix/mpc/v1/query-trade` 查询确认结果。
- (微信子链路)pix 先向 Tenpay 发起扫码支付,再经 [[svc_tradeii]] `createCashierTrade` 落库;create-trade 与 complete cashier flow 为两个独立步骤。
