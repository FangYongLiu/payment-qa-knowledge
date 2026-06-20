---
title: ENBD渠道总览
domain: channel-integration
kind: wiki_page
slug: enbd-channel-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道总览

本页汇总 ENBD 渠道相关的 PRD 入口、测试 IBAN、出款流程要点与账户配置，作为 ENBD 渠道知识的导航页。

## PRD 文档入口

- Fund out PRD: https://algento.atlassian.net/wiki/x/P4DGJQ
- Counter PRD: https://algento.atlassian.net/wiki/x/PgBfJg
- 个人提现部分 PRD: https://algento.atlassian.net/wiki/spaces/BOT/pages/732168261/ENBD

## 测试环境测试 IBAN

- EBILAED：`AE780260001015795438201`
- MEBLAED：`AE800340003707336602101`
- FGBMAEAA：`AE780271091001071667018`

## 渠道余额查询机制

通过 `balanceMonitorJob` 定时任务读取 `reconciliation.t_balance_monitor` 中状态=Y 的数据，调用 cmf（参数：渠道号、账户类型、银行、阈值），cmf 调用 router；router 根据 `channelCode`、`apiType=DB` 找到渠道，拿渠道对应账户去查询余额。

- 余额查询规则配置入口：counter → account → balance monitor。
  - **一期限制**：因为规则和交易阈值共用数据，所以规则**一个账户只能配置一条**。
- 规则落库表：`reconciliation.t_balance_monitor`。
- 渠道真实查询账户配置查询 SQL：

  ```sql
  select * from router.t_channel_ext
  where channel_code in ('ENBD201','ENBD204','ENBD205')
    and attr_key = 'payoutAccount';
  ```

- Job 触发余额查询，日志关键字：`开始`、`余额监控`、`定时任务`。
- 查询结果落库 `reconciliation.t_balance_history`（余额没有变化时不会新增数据）。
- 同时写入 Redis 缓存：`_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）。

详细逻辑见 [[auto_enbd_balance_monitor_job]]。

## 出款流程

总体链路：fundout → cmf → router。router 路由渠道时，判断渠道 ext 是否配置 `payoutAccount`：已配置则进行渠道余额校验，未配置则跳过。

### 1. 渠道与银行交互

- ENBD 渠道先发送 SP，银行返回 `httpResponseStatus=202`，表示已接收到请求、订单处理中。
- Payby 主动调用查询接口，银行可能返回的状态：
  - `ACCEPTED`
  - `IN_PROGRESS`（Transaction is in progress at the bank）
  - `PROCESSED_BY_BANK`
  - `COMPLETED`
- 银行通过状态变更通知推送最终结果。

### 2. 必填字段：countryCode / cityCode 获取逻辑

ENBD 和 INNER 卡类型均无需传 `cityCode`，因此只有**他行 IBAN**才会调用 member 查询 city name。

### 3. Remark 字段拼装规则

a. 默认使用 `memo` 字段（提现：Fundout）。
b. `memo` 为空时，使用 `purposeCode`：`FIS`（提现）/ `MWO`（转账到卡）；目前暂无为空场景。
c. 在 `useMerchantName` 配置中的商户，`memo` 使用「商户名称 + 地址」。
d. 在 `merchantDynamic` 配置中的商户，直接替换 `memo` 内容。

完整字段细节见 [[enbd-fundout-field-logic]]，整体流程见 [[flow_enbd_fundout]]。

## 渠道账户配置

ENBD 渠道按业务场景（商户出款 / 个人出款 / 资金调拨）和卡类型（INNER / DFT / IFT）拆分多个 channelCode，每个 channelCode 对应不同的待清算账户与银存账户：

| CASE | Channel Code | 待清算账户 | 银存账户 |
|---|---|---|---|
| 商户出款 | ENBD201（INNER – ENBD 卡） | 78430030040040001 FundOut Pending for Clearing-CMA4-ENBD201 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| 商户出款 | ENBD202（DFT – 非 ENBD 本地卡） | 78430030040040002 FundOut Pending for Clearing-CMA4-ENBD202 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| 商户出款 | ENBD203（IFT – 国际卡） | 78430030040040003 FundOut Pending for Clearing-CMA4-ENBD203 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| 个人出款 | ENBD204（INNER – ENBD 卡） | 78430030040020001 FundOut Pending for Clearing-CMA2-ENBD204 | 78410010170010002 Cash in Banks-ENBD CMA2 |
| 个人出款 | ENBD205（DFT – 非 ENBD 本地卡） | 78430030040020002 FundOut Pending for Clearing-CMA2-ENBD205 | 78410010170010002 Cash in Banks-ENBD CMA2 |
| 资金调拨 | ENBD209（INNER – ENBD 卡） | 78430030040030001 FundOut Pending for Clearing-CMA3-ENBD209 | 78410010170010003 Cash in Banks-ENBD CMA3 |
| 资金调拨 | ENBD210（DFT – 非 ENBD 本地卡） | 78430030040030002 FundOut Pending for Clearing-CMA3-ENBD210 | 78410010170010003 Cash in Banks-ENBD CMA3 |

## 常见问题（Q&A）

**Q：router 日志提示 ENBD 渠道 `channel account balance is not enough`。**

A：通过 counter 或 Redis 确认余额查询是否正常；如果余额正常，可尝试再次发起出款，可能当时对方系统有波动。

完整排查思路见 [[ts_enbd_channel_balance_not_enough]]。
