---
id: flow_enbd_fundout
object_type: Flow
name: ENBD 渠道出款流程(含账户映射 / 余额监控)
aliases: [ENBD出款, ENBD fundout]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1064206364
tags: [enbd, fundout, 出款, 余额监控, 账户映射]
related_services: [svc_qpay_enbd]
related_tables: []
related_scenarios: []
---

# ENBD 渠道出款流程(含账户映射 / 余额监控)

## 概述
ENBD 出款由 fundout 经 cmf 路由到 router,router 根据渠道配置决定是否进行余额校验,再与银行进行**异步状态交互**。ENBD 渠道按业务场景(商户出款/个人出款/资金调拨)和卡类型(INNER/DFT/IFT)拆分多个 channelCode(ENBD201–ENBD210),各对应不同的待清算账户与银存账户。余额由定时任务 `balanceMonitorJob` 周期性查询并落库+写 Redis,供出款时校验。

## 步骤(跨系统)
1. **调用链路**:[[svc_qpay_enbd]] fundout → cmf → router;router 按渠道路由到具体账户。
2. **余额校验判定**:router 判断渠道 ext(`router.t_channel_ext`)是否配置 `payoutAccount`:
   - 有配置:进行渠道余额校验(依赖余额监控,见下)。
   - 无配置:跳过余额校验。
3. **渠道与银行交互(异步)**:
   - ENBD 渠道先发送 SP,银行返回 `httpResponseStatus=202`(已接收,处理中)。
   - PayBy 主动调用查询接口,银行可能返回:`ACCEPTED` / `IN_PROGRESS` / `PROCESSED_BY_BANK` / `COMPLETED`。
   - 银行通过状态变更通知主动推送最终状态。
4. **余额监控(balanceMonitorJob)**:
   - reconciliation 读取 `reconciliation.t_balance_monitor` 中状态=Y 的规则。
   - 调用 cmf(参数:渠道号、账户类型、银行、阈值)→ cmf 调 router(`channelCode` + `apiType=DB` 找渠道)→ 拿渠道账户查余额。
   - 落库 `reconciliation.t_balance_history`(**余额无变化不新增数据**)+ 写 Redis 缓存 `_cmf:accountBalance:XXXXX`(XXXXX 为渠道账号)。
   - 日志关键字:`开始`、`余额监控`、`定时任务`。配置入口:counter – account – balance monitor。⚠️ 一期规则和交易阈值共用数据,**一个账户只能配置一条规则**。

## 字段规则
### countryCode / cityCode
- 由渠道侧获取;ENBD 和 INNER 渠道无需传 cityCode;仅他行 IBAN 场景渠道才调 member 查 city name。

### Remark 字段(按优先级)
- a. 默认用 memo 字段(提现场景:`Fundout`)。
- b. memo 为空时用 purposeCode:`FIS`=提现,`MWO`=转账到卡(目前暂无 memo 为空场景)。
- c. 命中 `useMerchantName` 配置的商户:memo=商户名称+地址。
- d. 命中 `merchantDynamic` 配置的商户:直接替换 memo 内容。

## 渠道账户映射表
| Channel Code | 场景 | 卡类型 | 待清算账户 | 银存账户 |
|---|---|---|---|---|
| ENBD201 | 商户出款 CMA4 | INNER–ENBD 卡 | 78430030040040001 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| ENBD202 | 商户出款 CMA4 | DFT–非 ENBD 本地卡 | 78430030040040002 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| ENBD203 | 商户出款 CMA4 | IFT–国际卡 | 78430030040040003 | 78410010170010004 Cash in Banks-ENBD CMA4 |
| ENBD204 | 个人出款 CMA2 | INNER–ENBD 卡 | 78430030040020001 | 78410010170010002 Cash in Banks-ENBD CMA2 |
| ENBD205 | 个人出款 CMA2 | DFT–非 ENBD 本地卡 | 78430030040020002 | 78410010170010002 Cash in Banks-ENBD CMA2 |
| ENBD209 | 资金调拨 CMA3 | INNER–ENBD 卡 | 78430030040030001 | 78410010170010003 Cash in Banks-ENBD CMA3 |
| ENBD210 | 资金调拨 CMA3 | DFT–非 ENBD 本地卡 | 78430030040030002 | 78410010170010003 Cash in Banks-ENBD CMA3 |

映射规则:账户后缀按业务域(商户 CMA4 / 个人 CMA2 / 调拨 CMA3);ChannelCode 按交易类型(INNER / DFT / IFT,IFT 仅商户出款支持)。
渠道真实查询账户配置 SQL:
```sql
select * from router.t_channel_ext
where channel_code in ('ENBD201','ENBD204','ENBD205')
  and attr_key = 'payoutAccount';
```

## 关联关系
- **经过的服务(有序)**:[[svc_qpay_enbd]] → cmf → router → 银行(= `related_services`;cmf/router/reconciliation 对象待补)
- **关键表**:`router.t_channel_ext`、`reconciliation.t_balance_monitor`、`reconciliation.t_balance_history`(对象待补)
- **排查**:出款报余额不足见 [[ts_enbd_channel_balance_not_enough]]

## 校验点
- 渠道是否参与余额校验取决于 `t_channel_ext` 是否配 `payoutAccount`;未配则跳过。
- 余额历史表余额无变化不新增;Redis 缓存 key `_cmf:accountBalance:XXXXX`。
- 与银行异步交互状态流转(202 → ACCEPTED → IN_PROGRESS → PROCESSED_BY_BANK → COMPLETED)。

## 参考资料
- Fund out PRD:https://algento.atlassian.net/wiki/x/P4DGJQ;Counter PRD:https://algento.atlassian.net/wiki/x/PgBfJg;个人提现 PRD:https://algento.atlassian.net/wiki/spaces/BOT/pages/732168261/ENBD
- 测试环境 IBAN:EBILAED `AE780260001015795438201`;MEBLAED `AE800340003707336602101`;FGBMAEAA `AE780271091001071667018`
