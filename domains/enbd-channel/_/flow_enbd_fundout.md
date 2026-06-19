---
id: flow_enbd_fundout
object_type: Flow
domain: channel-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/1064206364
tags:
- fundout
- ENBD
- router
- cmf
subdomain: null
module: fundout
sensitivity: normal
name: ENBD渠道出款流程
aliases: []
related_services: []
related_tables:
- router.t_channel_ext
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- ts_enbd_channel_balance_not_enough
---

## 概述
ENBD渠道出款端到端流程：fundout → cmf → router → ENBD银行。router 路由渠道时，会判断渠道 ext 是否配置了 payoutAccount，若配置则进行渠道余额校验，否则跳过校验后与 ENBD 银行交互。

## 步骤(跨系统)
1. fundout 调用 cmf。
2. cmf 调用 router。
3. router 路由渠道，查询 `router.t_channel_ext` 中 `attr_key='payoutAccount'` 的配置：
   - 已配置 payoutAccount：进行渠道余额校验（基于 balanceMonitorJob 落地的余额数据 / redis 缓存 `_cmf:accountBalance:XXXXX`）。
   - 未配置：跳过余额校验。
4. 渠道与银行交互：
   a. ENBD 渠道先发送 SP，银行返回 `httpResponseStatus=202` —— 表示接收到请求，订单处理中。
   b. Payby 主动调用查询接口，银行可能返回：`ACCEPTED`、`IN_PROGRESS`（Transaction is in progress at the bank）、`PROCESSED_BY_BANK`、`COMPLETED`。
   c. 银行发状态变更通知。
5. 渠道必填字段 country Code、city Code 获取逻辑：ENBD 和 INNER 无需传 citycode；只有他行 IBAN 才会调用 member 查询 city name。
6. Remark 字段逻辑：
   a. 默认使用 memo 字段（提现：Fundout）。
   b. memo 为空时使用 FIS / MWO（purposeCode：FIS=提现，MWO=转账到卡）。
   c. 在 useMerchantName 配置中的商户，memo 使用 商户名称+地址。
   d. 在 merchantDynamic 配置中的商户，直接替换 memo 内容。

## 涉及服务/表
- 服务：fundout、cmf、router、member（仅他行 IBAN 查询 city name 时调用）
- 表：`router.t_channel_ext`（`attr_key='payoutAccount'`，channel_code 包含 ENBD201 / ENBD204 / ENBD205 等）
- 缓存：redis `_cmf:accountBalance:XXXXX`
- 渠道场景与账户：
  - 商户出款：ENBD201(INNER-ENBD卡)、ENBD202(DFT-非ENBD本地卡)、ENBD203(IFT-国际卡)，待清算账户 7843003004004000x，银存账户 78410010170010004（Cash in Banks-ENBD CMA4）
  - 个人出款：ENBD204(INNER-ENBD卡)、ENBD205(DFT-非ENBD本地卡)，银存账户 78410010170010002（Cash in Banks-ENBD CMA2）
  - 资金调拨：ENBD209(INNER-ENBD卡)、ENBD210(DFT-非ENBD本地卡)，银存账户 78410010170010003（Cash in Banks-ENBD CMA3）

## 校验点
- router 检查渠道 ext 是否配置 payoutAccount 决定是否进行余额校验。
- 渠道余额不足会在 router 日志中提示：`channel account balance is not enough.`，可通过 counter 或 redis 确认余额查询是否正常；若余额正常则可再次发起出款（可能对方系统波动）。详见 [[ts_enbd_channel_balance_not_enough]]。
- 渠道必填字段 country Code / city Code 校验（ENBD、INNER 不需要 citycode）。
- 银行回执状态流转校验：`httpResponseStatus=202` → `ACCEPTED`/`IN_PROGRESS`/`PROCESSED_BY_BANK`/`COMPLETED`，并以银行状态变更通知为准。
