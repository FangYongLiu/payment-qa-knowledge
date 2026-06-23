---
title: 支付渠道号PayChannelNo说明
domain: acquire-transaction
kind: wiki_page
slug: acquire-pay-channel-no
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997851554
tags: []
---

# 支付渠道号PayChannelNo说明

PayChannelNo 用于标识收单交易所使用的具体支付渠道类型，覆盖网银、余额、卡组织、第三方钱包等多种资金来源。

## 渠道号对照表

| Pay Channel No | Description |
| --- | --- |
| 04 | 对私网银 |
| 12 | 对公网银 |
| 14 | 余额 |
| 15 | 快捷支付 |
| 16 | 线下汇款 |
| 17 | MOTO |
| 18 | KIOSK |
| 20 | PayLater |
| 21 | ALIPAY |
| 22 | GP抵扣 |
| 23 | GP支付 |
| 30 | 国际卡 |

## 相关说明

- 与支付场景码搭配使用，定位一笔交易的场景与渠道组合，详见 [[acquire-pay-scene-code]]。
- 收单交易完整流程参见 [[acquire-transaction-overview]]。
