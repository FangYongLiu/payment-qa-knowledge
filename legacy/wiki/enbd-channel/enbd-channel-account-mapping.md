---
title: ENBD渠道账户映射表
domain: channel-integration
kind: wiki_page
slug: enbd-channel-account-mapping
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道账户映射表

本页汇总 ENBD 各 ChannelCode 对应的业务场景、待清算账户与银存账户配置，用于出款记账与对账核对。相关流程见 [[enbd-channel-fundout-flow]]，余额查询见 [[enbd-channel-balance-monitor]]。

## 商户出款（CMA4）

| Channel Code | 场景 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD201 | INNER – ENBD 卡 | 78430030040040001 FundOut Pending for Clearing-CMA4-ENBD201 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| ENBD202 | DFT – 非 ENBD 本地卡 | 78430030040040002 FundOut Pending for Clearing-CMA4-ENBD202 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| ENBD203 | IFT – 国际卡 | 78430030040040003 FundOut Pending for Clearing-CMA4-ENBD203 | 78410010170010004 Cash in Banks-ENBD CMA4 |

- 商户出款三种渠道共用同一银存账户 `Cash in Banks-ENBD CMA4`。

## 个人出款（CMA2）

| Channel Code | 场景 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD204 | INNER – ENBD 卡 | 78430030040020001 FundOut Pending for Clearing-CMA2-ENBD204 | 78410010170010002 Cash in Banks-ENBD CMA2 |
| ENBD205 | DFT – 非 ENBD 本地卡 | 78430030040020002 FundOut Pending for Clearing-CMA2-ENBD205 | 78410010170010002 Cash in Banks-ENBD CMA2 |

- 个人出款两种渠道共用同一银存账户 `Cash in Banks-ENBD CMA2`。

## 资金调拨（CMA3）

| Channel Code | 场景 | 待清算账户 | 银存账户 |
|---|---|---|---|
| ENBD209 | INNER – ENBD 卡 | 78430030040030001 FundOut Pending for Clearing-CMA3-ENBD209 | 78410010170010003 Cash in Banks-ENBD CMA3 |
| ENBD210 | DFT – 非 ENBD 本地卡 | 78430030040030002 FundOut Pending for Clearing-CMA3-ENBD210 | 78410010170010003 Cash in Banks-ENBD CMA3 |

- 资金调拨两种渠道共用同一银存账户 `Cash in Banks-ENBD CMA3`。

## 渠道与场景映射规则

- 按业务域划分账户后缀：商户出款 → CMA4，个人出款 → CMA2，资金调拨 → CMA3。
- 按交易类型划分 ChannelCode：
  - INNER：ENBD 卡内部转账（ENBD201 / ENBD204 / ENBD209）
  - DFT：非 ENBD 本地卡（ENBD202 / ENBD205 / ENBD210）
  - IFT：国际卡，仅商户出款支持（ENBD203）

## 渠道真实查询账户配置

查询渠道在 router 中配置的实际余额查询账户：

```sql
select * from router.t_channel_ext
where channel_code in ('ENBD201','ENBD204','ENBD205')
and attr_key ='payoutAccount';
```

- 仅当渠道 ext 配置了 `payoutAccount` 时，出款链路才会进行渠道余额校验，否则跳过。

## 相关链接

- 总览：[[enbd-channel-overview]]
- 余额监控：[[enbd-channel-balance-monitor]]
- 出款流程：[[enbd-channel-fundout-flow]]
- 问题排查：[[enbd-channel-troubleshooting]]
