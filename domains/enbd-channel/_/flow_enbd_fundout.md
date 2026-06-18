---
id: flow_enbd_fundout
object_type: Flow
domain: enbd-channel
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags:
- fundout
- ENBD
- router
- cmf
subdomain: null
module: null
sensitivity: normal
name: ENBD出款端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ENBD出款端到端流程：fundout 调用 cmf，cmf 调用 router；router 路由渠道并判断渠道 ext 是否配置 payoutAccount，若配置则进行渠道余额校验，否则跳过。随后由 ENBD 渠道与银行进行 SP 请求、查询、状态通知交互，完成订单状态流转。

## 步骤(跨系统)
1. fundout → cmf → router：router 根据渠道路由，判断渠道 ext 是否配置 `payoutAccount`；已配置则进行渠道余额校验，未配置则跳过。
2. 渠道与银行交互：
   - a. ENBD 渠道先发送 SP，银行返回 `httpResponseStatus=202`（接受请求，订单处理中）。
   - b. Payby 主动调用查询接口，银行可能返回：`ACCEPTED`、`IN_PROGRESS`(Transaction is in progress at the bank)、`PROCESSED_BY_BANK`、`COMPLETED`。
   - c. 银行发状态变更通知。
3. 渠道必填字段处理：
   - countryCode、cityCode 按渠道逻辑获取。
   - ENBD 与 INNER 无需传 cityCode；只有他行 IBAN 才会调用 member 查询 city name。
4. Remark 字段逻辑：
   - a. 默认使用 memo 字段（提现：Fundout）。
   - b. memo 为空时使用 purposeCode：FIS（提现）/ MWO（转账到卡）。
   - c. 命中 `useMerchantName` 配置的商户，memo 使用 商户名称+地址。
   - d. 命中 `merchantDynamic` 配置的商户，直接替换 memo 内容。

## 涉及服务/表
- 服务链路：fundout → cmf → router → ENBD 银行
- 渠道账户配置查询：
  ```
  select * from router.t_channel_ext
  where channel_code in ('ENBD201','ENBD204','ENBD205')
  and attr_key ='payoutAccount'
  ```
- 渠道与会计科目对应：
  - 商户出款：ENBD201(INNER-ENBD卡)、ENBD202(DFT-非ENBD本地卡)、ENBD203(IFT-国际卡) → 待清算账户 7843003004004000x / 银存账户 78410010170010004 (Cash in Banks-ENBD CMA4)
  - 个人出款：ENBD204(INNER)、ENBD205(DFT) → 待清算 7843003004002000x / 银存账户 78410010170010002 (Cash in Banks-ENBD CMA2)
  - 资金调拨：ENBD209(INNER)、ENBD210(DFT) → 待清算 7843003004003000x / 银存账户 78410010170010003 (Cash in Banks-ENBD CMA3)

## 校验点
- router 校验渠道 ext `payoutAccount` 是否配置，决定是否做渠道余额校验。
- 银行返回 `httpResponseStatus=202` 表示接受请求/处理中；终态需通过查询或银行通知确认（`PROCESSED_BY_BANK` / `COMPLETED`）。
- 他行 IBAN 才需通过 member 查询 city name，ENBD/INNER 无需 cityCode。
- Remark 取值优先级：memo → purposeCode(FIS/MWO) → useMerchantName(商户名+地址) → merchantDynamic(替换 memo)。
- 若 router 日志报 `channel account balance is not enough`，需通过 counter 或 redis 确认余额查询是否正常；若余额正常可重试发起出款。
