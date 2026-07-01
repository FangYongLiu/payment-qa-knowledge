---
title: MG (MoneyGram) 渠道总览
domain: channel-integration
kind: wiki_page
slug: mg-channel-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268547712
tags: []
related_services:
  - svc_basis_customer
  - svc_bigdata_router
  - svc_remittance
related_tables:
  - tbl_remittance_t_channel_param_mapping
---

# MG (MoneyGram) 渠道总览

MG 是 PayBy 接入的间接汇款渠道，覆盖大多数收款国家与币种，因不同国家所需字段差异较大，接入时增加了动态字段收集与实时汇率查询逻辑。

## 基础信息

- **渠道名称**：MG (MoneyGram)
- **直联 / 间接**：间接渠道
- **支持币种 / 国家**：覆盖范围广，支持大多数收款国家和币种
- **特殊说明**：不同国家所需汇款字段差异较大，需通过额外参数收集逻辑动态适配

## 接口清单

MG 渠道按用途分为四类接口，详细说明见各自子页：

### 汇率相关
- [[api_mg_fee_lookup]]：查询国家币种下支持的所有模式及汇率，**MG 必须实时请求**，不使用数据库静态汇率；模式下可能存在多个 agentid（钱包/bank 场景），通过 `t_channel_param_mapping` 表配置

### 信息收集
- [[api_mg_gffp]]：返回指定收款国家+币种下汇款需收集的字段，进入 Transfer Details 页面时调用，24 小时缓存
- [[api_mg_send_validation]]：下单前对金额、字段、合规性进行预校验，用户点击 Confirm 时触发，不通过则阻断交易

### 订单处理
- [[api_mg_commit]]：提交最终汇款订单，支付完成后由 Remittance 通知渠道下单
- [[api_mg_order_status_query]]：查询订单处理状态，由 Remittance 定时 Job 调用，需处理成功同步、失败退款、超 60 天未成功的 cash pick up 主动退款，以及 `PRCSS`（渠道审核中）、`AFR`（可触发退款）等特殊状态
- [[api_mg_send_reversal]]：主动退款接口，用于 cancel 操作、超 60 天未成功 cash pick up、`AFR` 状态等场景

### 入账与退款
- **Callback / Notification**：MG 无主动推送，依赖主动轮询查询订单状态
- **Refund Handling**：查询返回失败时由 Remittance 触发退款；MG 提供主动退款接口（SendReversal）
- **Funding flow**：下单成功推送入款的入账流水；主动退款或查询到失败退款时推送退款的入账流水

## 状态映射

MG 没有 sub state，state 与 sub state 设定为相同值。完整 PayBy ↔ MG 状态对照见 [[mg-channel-state-mapping]]。

## 异常与限制

### 超时与幂等
- MG 要求请求超时后须**按完全相同参数再次请求**，渠道侧具备幂等逻辑

### 金额限制
- MG 未直接提供金额限制，PayBy 通过定时脚本不断递增金额调用 MG 接口直至报错，获取到的限额配置在 bigdata router 的决策表中

### 国家差异化展示
- 部分国家要求在最终确认页展示 **estimated receive amount** 和 **estimated exchange rate**，依据 FeeLookup 接口返回的 `validCurrencyIndicator=false` 判断
- 部分国家要求在最终确认页展示 **Receiver's fee**，依据 FeeLookup 接口返回的 `<ac:totalReceiveFees>` 与 `<ac:totalReceiveTaxes>` 判断并展示

### 特殊订单处理
- **PRCSS（渠道审核中）**：需用户主动补充信息，前端有专门流程；可用印度 bank transfer 的 First Name: Buggs, Last Name: Bunny 复现
- **AFR**：查询到该状态可直接触发主动退款
- **成功后再失败**：MG 订单成功后仍可能转为失败，basis-customer 订单详情页对 MG 成功订单提供 **refresh 按钮**，点击重查状态，若变为 refund 则系统对该笔交易做退款处理
- **PICK_UP_EXPIRE（90 天未领取）**：MG 内部置为过期，查询返回 `Error=707, Message=Please call MoneyGram customer service center to complete this transaction (code 45)`；PayBy 将订单挂起为 `RS / PUE`，继续轮询，若已退款则 PayBy 同步退款
