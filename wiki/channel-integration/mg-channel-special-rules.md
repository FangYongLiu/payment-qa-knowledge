---
title: MG渠道特殊业务规则
domain: channel-integration
kind: wiki_page
slug: mg-channel-special-rules
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags: []
---

# MG渠道特殊业务规则

本页汇总 MG (MoneyGram) 渠道在金额限额获取、特定国家展示要求等方面的特殊业务逻辑，便于接入与测试时关注差异点。相关背景见 [[mg-channel-overview]]。

## 金额限额获取机制

- MG 未直接提供金额限额给我方。
- 通过定时脚本以完全相同参数不断递增金额调用 MG 接口，直到接口报错为止，从而推算出限额。
- 获取到的限额配置在 **bigdata router 的决策表**中，供路由决策使用。

## 请求超时与幂等

- MG 要求：请求超时时，需以**完全相同参数再次请求**。
- 接口侧具备幂等逻辑，重试不会造成重复下单。

## 特定国家展示要求

部分收款国家在最终确认页(Transfer Details / Confirm)上有额外字段展示要求，依据 `FeeLookup` 接口返回判定。

### Estimated Receive Amount / Estimated Exchange Rate

- **触发条件**：`FeeLookup` 接口返回 `validCurrencyIndicator=false`。
- **展示内容**：在最终确认页展示 `estimated receive amount` 与 `estimated exchange rate`。

### Receiver's Fee

- **触发条件**：`FeeLookup` 接口返回包含以下字段：
  - `<ac:totalReceiveFees>` (如 100)
  - `<ac:totalReceiveTaxes>` (如 5)
- **展示内容**：在最终确认页展示 `Receiver's fee`。

## 信息收集动态字段

- 不同国家所需收款人信息差异较大。
- 通过 `GFFP (Get Form Fields)` 接口返回的字段清单，与数据库已有字段比对；缺失字段在页面上动态展示补充输入框。
- `GFFP` 调用结果 24 小时内缓存，期间不再重复请求。

## 订单状态特殊处理

以下状态属于 MG 渠道独有的业务处理逻辑（完整映射见 [[mg-channel-state-mapping]]）：

- **PRCSS (渠道审核中)**：要求用户主动提交补充信息，前端已实现该流程。详细测试方法见 [[scn_mg_prcss_risk_review]]。
- **AFR**：可直接触发主动退款，查询到此状态即调用 `SendReversal`。
- **成功后再失败**：MG 订单在 `RECVD (Completed)` 之后仍可能失败转为退款。因此在 basis-customer 订单详情页，MG 成功订单提供 **refresh 按钮**，点击会重新查询订单状态；若变为 `REFND`，系统也会对该笔交易做退款处理。
- **超 60 天未领取的 cash pick up 订单**：查询状态仍为处理中时，需主动调用 `SendReversal` 发起退款。
- **PICK_UP_EXPIRE (90 天未领取)**：查询返回 `Error=707` 时，订单挂起为 `RS / PUE`，继续轮询；若 MG 已退款则我方同步退款。

## 入账与回调

- MG **无主动回调推送**，完全依赖我方主动轮询 `Order Status Query`。
- 资金流水推送时机：
  - 下单成功 → 推送入款流水。
  - 主动退款或查询到失败退款 → 推送退款流水。

完整端到端流程参考 [[flow_mg_remittance]]。
