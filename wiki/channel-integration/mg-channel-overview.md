---
title: MG (MoneyGram) 渠道总览
domain: channel-integration
kind: wiki_page
slug: mg-channel-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags: []
---

# MG (MoneyGram) 渠道总览

MG 是一条间接渠道，覆盖国家与币种范围广，因不同国家收款字段差异较大，接入时增加了额外的参数收集逻辑，并依赖主动轮询同步订单状态。

## 基础信息

- **渠道名称**：MG (MoneyGram)
- **直联 / 间接**：间接渠道
- **支持币种 / 国家**：覆盖范围广，支持大多数收款国家和币种
- **特殊说明**：不同国家需要的字段差异较大，因此接入时增加了额外的参数收集逻辑

## 接口清单

### 汇率相关接口

**FeeLookup**
- 作用：查询国家币种下支持的所有模式及该模式下的汇率；同一模式下可能有多个 agentid（钱包和 bank 场景下使用，不同钱包走不同 agentid），提前在 `t_channel_param_mapping` 表里配置
- 调用时机：用户点击 Send Money，完成路由后渠道为 MG 时调用
- 特殊逻辑：与数据库静态汇率不同，MG 必须实时请求

### 信息收集接口

**GFFP (Get Form Fields)**
- 作用：返回指定收款国家+币种下汇款需要收集的所有字段
- 调用时机：用户进入 Transfer Details 页面时，24 小时内调用一次，结果存入缓存，之后从缓存取
- 特殊逻辑：比对数据库已有字段，缺失字段在页面动态展示补充输入框

**SendValidation (Pre-Validation)**
- 作用：下单前对交易请求进行预校验（金额、字段、合规性等）
- 调用时机：用户在 Transfer Details 页面点击 Confirm 时
- 特殊逻辑：不通过时直接阻断交易，返回具体错误

### 订单处理接口

**commit（下单接口）**
- 作用：提交最终的汇款订单
- 调用时机：支付完成后，Remittance 通知渠道下单
- 说明：成功返回后系统进入结算流程

**Order Status Query**
- 作用：查询订单处理状态（成功 / 失败 / 审核中）
- 调用时机：由 Remittance 的定时 Job 调用
- 需处理的状态：
  1. 成功订单：更新订单、同步账单等
  2. 失败订单：触发退款逻辑
  3. 超 60 天未成功的 cash pick up 订单：等同于主动发起退款，调对方主动退款接口
- 特殊状态：
  - **PRCSS**：渠道审核中，要求用户主动提交信息，前端有相应流程；测试可用印度 bank transfer，First Name: `Buggs`，Last Name: `Bunny` 去 MG 汇款，几分钟后自动变为 PRCSS（参见 [[scn_mg_prcss_risk_review]]）
  - **AFR**：可直接触发退款的状态，查询到即触发主动退款
  - MG 订单成功后仍可能失败，故 customer 订单详情页面对 MG 成功订单提供 refresh 按钮，点击重新查询；若变为 refund，则系统对该笔交易做退款处理

**SendReversal（主动退款）**
- 作用：主动退款
- 调用时机：
  1. basis-customer 订单详情页展示 cancel 按钮触发
  2. 超 60 天未成功的 cash pick up 订单查询仍处理中时发起退款
  3. 查询到订单处于 AFR 状态时发起退款
- 说明：失败订单需触发退款逻辑

> 订单状态映射详见 [[mg-channel-state-mapping]]。

### 入账与退款相关

- **Callback / Notification**：MG 无主动推送，依赖主动轮询查询订单状态
- **Refund Handling**：查询返回失败时由 Remittance 触发退款；MG 提供主动退款接口
- **Funding flow**：下单成功后推送入款的入账流水；主动退款或查询到失败退款后，推送退款的入账流水

## 异常与限制

- **超时处理**：MG 要求请求超时后按完全相同参数再次请求，具备幂等逻辑
- **金额限额**：MG 未直接提供限额，依赖定时脚本不停增加金额调用 MG 接口直到报错获取，配置在 bigdata router 的决策表中
- **展示要求**（详见 [[mg-channel-special-rules]]）：
  - 部分国家要求在最终确认页展示 estimated receive amount 与 estimated exchange rate，依据 FeeLookup 接口的 `validCurrencyIndicator=false` 判定
  - 部分国家要求在最终确认页展示 Receiver's fee，依据 FeeLookup 返回的 `<ac:totalReceiveFees>` 与 `<ac:totalReceiveTaxes>` 判定并展示

## 相关页面

- [[flow_mg_remittance]]：MG 汇款端到端流程
- [[mg-channel-state-mapping]]：订单状态映射表
- [[mg-channel-special-rules]]：特殊业务规则
- [[scn_mg_prcss_risk_review]]：PRCSS 风控审核场景测试
