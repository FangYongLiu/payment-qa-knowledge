---
title: ENBD渠道总览
domain: enbd-channel
kind: wiki_page
slug: enbd-channel-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags: []
---

# ENBD渠道总览

本页汇总 ENBD 渠道的 PRD 入口、测试环境 IBAN 以及渠道分类与待清算/银存账户配置一览，便于快速定位资料和账户对照关系。

## PRD 文档入口

- Fund out PRD：https://algento.atlassian.net/wiki/x/P4DGJQ
- Counter PRD：https://algento.atlassian.net/wiki/x/PgBfJg
- 个人提现部分 PRD：https://algento.atlassian.net/wiki/spaces/BOT/pages/732168261/ENBD

## 测试环境测试 IBAN

- EBILAED：`AE780260001015795438201`
- MEBLAED：`AE800340003707336602101`
- FGBMAEAA：`AE780271091001071667018`

## 渠道分类与账户配置一览

ENBD 渠道按业务场景分为商户出款、个人出款、资金调拨三类，每类下又按 INNER（ENBD 卡）/DFT（非 ENBD 本地卡）/IFT（国际卡）细分。

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

## 渠道真实查询账户

通过 router 配置查询渠道对应的真实查账账户：

```sql
select * from router.t_channel_ext
where channel_code in ('ENBD201','ENBD204','ENBD205')
  and attr_key = 'payoutAccount'
```

## 关联页面

- [[enbd-balance-monitor-job]]：渠道余额查询 Job 流程与落库逻辑
- [[enbd-fundout-flow]]：出款流程、渠道交互与字段逻辑
- [[enbd-channel-troubleshooting]]：常见问题排查（如余额不足提示）

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>
