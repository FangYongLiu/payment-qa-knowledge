---
title: ENBD渠道常见问题排查
domain: enbd-channel
kind: wiki_page
slug: enbd-channel-troubleshooting
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道常见问题排查

本页汇总 ENBD 渠道在出款过程中常见报错的定位思路与处置方法，主要面向 router 校验失败、余额查询异常等场景。相关背景见 [[enbd-channel-overview]]、[[enbd-channel-balance-monitor]]、[[enbd-channel-fundout-flow]]。

## channel account balance is not enough

router 日志出现 `ENBD 渠道 channel account balance is not enough` 报错时的处理：

- 先确认余额查询是否正常，可通过两种方式核对：
  - 查询 counter 中该渠道账户的最新余额数据
  - 查询 redis 缓存 key：`_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）
- 若余额数据正常（充足且与实际相符），可再次发起出款，可能是当时对方系统波动导致的瞬时校验失败
- 余额查询机制与缓存逻辑详见 [[enbd-channel-balance-monitor]]
- 详细排查步骤见 [[ts_enbd_channel_balance_not_enough]]

## 排查切入点

遇到 ENBD 出款异常时，建议按以下顺序定位：

1. **确认渠道是否配置 payoutAccount**：router 仅在 `router.t_channel_ext` 配置了 `payoutAccount` 的渠道上做余额校验，未配置则跳过。
   ```sql
   select * from router.t_channel_ext
   where channel_code in ('ENBD201','ENBD204','ENBD205')
     and attr_key = 'payoutAccount'
   ```
2. **确认余额监控 job 是否正常运行**：日志关键字「开始 余额监控 定时任务」，落库表 `reconciliation.t_balance_history`（余额无变化不会新增），参见 [[auto_enbd_balance_monitor_job]]。
3. **确认 balance monitor 规则配置**：通过 counter – account – balance monitor 配置，注意一期规则和交易阈值共用数据，**一个账户只能配置一条规则**。
4. **确认渠道与银行交互状态**：参见 [[flow_enbd_fundout]] 中的状态流转（`httpResponseStatus=202` / `ACCEPTED` / `IN_PROGRESS` / `PROCESSED_BY_BANK` / `COMPLETED`）。

## 测试环境可用 IBAN

排查或复现问题时，可使用以下测试环境 IBAN：

- EBILAED：`AE780260001015795438201`
- MEBLAED：`AE800340003707336602101`
- FGBMAEAA：`AE780271091001071667018`

## 关联信息

- 渠道与待清算/银存账户对照见 [[enbd-channel-account-mapping]]
- 出款字段规则（cityCode、Remark 等）见 [[enbd-channel-fundout-flow]]
