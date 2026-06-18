---
title: ENBD出款流程与字段逻辑
domain: enbd-channel
kind: wiki_page
slug: enbd-fundout-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags: []
---

# ENBD出款流程与字段逻辑

本页说明 ENBD 出款链路（fundout → cmf → router）的银行交互状态、必填字段获取、Remark 拼装规则，以及不同场景的渠道与账户对应关系。

## 出款链路

- 调用链：fundout 调用 cmf，cmf 调用 router
- router 路由渠道，判断渠道 ext 是否有配置 `payoutAccount`
  - 配置了：进行渠道余额校验（参考 [[enbd-balance-monitor-job]]）
  - 未配置：跳过余额校验
- 端到端流程详见 [[flow_enbd_fundout]]

## 渠道与银行交互状态

1. ENBD 渠道先发送 SP，银行返回 `httpResponseStatus=202`，表示已接收请求、订单处理中
2. Payby 主动调用查询接口，银行可能返回：
   - `ACCEPTED`
   - `IN_PROGRESS`（Transaction is in progress at the bank）
   - `PROCESSED_BY_BANK`
   - `COMPLETED`
3. 银行通过状态变更通知推送最终结果

## 渠道必填字段

- 必填：`countryCode`、`cityCode`
- 获取逻辑：
  - ENBD 与 INNER 场景无需传 `cityCode`
  - 仅当为他行 IBAN 时，才会调用 member 查询 city name

## Remark 字段逻辑

按以下优先级拼装 remark：

1. 默认使用 `memo` 字段（提现：Fundout）
2. `memo` 为空时，使用 `purposeCode`：
   - `FIS`：提现
   - `MWO`：转账到卡
   - （目前暂无为空场景）
3. 命中 `useMerchantName` 配置的商户：`memo` = 商户名称 + 地址
4. 命中 `merchantDynamic` 配置的商户：直接替换 `memo` 内容

## 渠道与账户对应关系

### 商户出款

| Channel Code | 类型 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD201 | INNER – ENBD 卡 | 78430030040040001 / FundOut Pending for Clearing-CMA4-ENBD201 | 78410010170010004 / Cash in Banks-ENBD CMA4 |
| ENBD202 | DFT – 非 ENBD 本地卡 | 78430030040040002 / FundOut Pending for Clearing-CMA4-ENBD202 | 78410010170010004 / Cash in Banks-ENBD CMA4 |
| ENBD203 | IFT – 国际卡 | 78430030040040003 / FundOut Pending for Clearing-CMA4-ENBD203 | 78410010170010004 / Cash in Banks-ENBD CMA4 |

### 个人出款

| Channel Code | 类型 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD204 | INNER – ENBD 卡 | 78430030040020001 / FundOut Pending for Clearing-CMA2-ENBD204 | 78410010170010002 / Cash in Banks-ENBD CMA2 |
| ENBD205 | DFT – 非 ENBD 本地卡 | 78430030040020002 / FundOut Pending for Clearing-CMA2-ENBD205 | 78410010170010002 / Cash in Banks-ENBD CMA2 |

### 资金调拨

| Channel Code | 类型 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD209 | INNER – ENBD 卡 | 78430030040030001 / FundOut Pending for Clearing-CMA3-ENBD209 | 78410010170010003 / Cash in Banks-ENBD CMA3 |
| ENBD210 | DFT – 非 ENBD 本地卡 | 78430030040030002 / FundOut Pending for Clearing-CMA3-ENBD210 | 78410010170010003 / Cash in Banks-ENBD CMA3 |

## 测试环境测试 IBAN

- EBILAED：`AE780260001015795438201`
- MEBLAED：`AE800340003707336602101`
- FGBMAEAA：`AE780271091001071667018`

## 相关

- 渠道总览：[[enbd-channel-overview]]
- 出款前余额校验依赖：[[enbd-balance-monitor-job]]
- 异常排查（如 `channel account balance is not enough`）：[[enbd-channel-troubleshooting]]
