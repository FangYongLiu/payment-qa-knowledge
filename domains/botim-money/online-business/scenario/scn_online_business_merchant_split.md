---
id: scn_online_business_merchant_split
object_type: Scenario
name: 商户分账 (Merchant Split)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_merchant_split_fangyong.py (UAT 实跑 2026-07-03, N101 PASSED)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_acquireii, svc_tradeii, svc_payment, svc_pfs_payment, svc_merchant]
related_tables: [tbl_acquireii_t_sharing_info, tbl_acquireii_t_acquire_order, tbl_tradeii_t_trade_order]
related_logs: []
---

# 商户分账 (Merchant Split)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 商户分账:一笔交易按规则分账到多个商户,含分账退款(refundSharingAmount)。经 tradeii/payment + pfs 清分。

## 关联关系
- **涉及服务**:[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_pfs_payment]]、[[svc_merchant]](= `related_services`,穿过的服务链)
- **读写的表**:[[tbl_acquireii_t_sharing_info]] 分账信息(order_id / sharing_mid / sharing_amount / sharing_settled_amount / sharing_settled_fee_amt)。

## 下单分账参数(实测请求结构)
`placeOrder` 顶层 `sharingInfoList`(PAYPAGE 分账):每项 `sharingIdentitySeqId`(序号,从 1)、`sharingMid`(分账收款方,如 200000087655)、`sharingAmount={amount,currency}`、`sharingMemo`、可选 `withholdAndRemitFee`(true=该方承担手续费)。成功后落 [[tbl_acquireii_t_sharing_info]]:`sharing_settled_amount` = 分得金额、`sharing_settled_fee_amt`。

## 实测结论(UAT 2026-07-03,已核实)
**基础分账在 UAT 可用,无需子商户特殊配置**:N101(主商户 `200000080798` → 分账方 `200000087655`,8 元分 4)**下单返回 CREATED(带 `sharingInfoList`)→ 轮询 SETTLED**,交易 [[tbl_tradeii_t_trade_order]] `trade_status=SS`、收单 [[tbl_acquireii_t_acquire_order]] `SETTLED`(product 200101/PAYPAGE),分账落 [[tbl_acquireii_t_sharing_info]](`sharing_mid`/`sharing_amount`/`sharing_settled_amount`)+ 分账方 `dpm.t_dpm_outer_account_subset` 余额增加——全链路通。

**先前"14 failed"根因(已细化,2026-07-04):两类,均非无分账能力**:
1. **测试数据缺口**(仅 N103/N109):`test_data_uat.yml` 只定义 `test_merchantSplit_N101`,而 N103/N109 读 `test_merchantSplit_N103`(多分账方,需 `sharingMid2`)→ `KeyError`。已补该 key(sharingMid2=`200000091441`,UAT 核验有效 AED 账户)。N102/N104–N110 本就复用 N101 数据,无缺口。
2. **⚠️ 产品行为 —— `withholdAndRemitFee=True` 分账单在 UAT 直接 FAILURE**(需 dev 确认):**决定性对照**——N101(单分账方,**无** withhold)→ SETTLED;N102(**完全相同数据**,body 仅加 `withholdAndRemitFee=True`)→ 下单即 `status=FAILURE`(`head` SUCCESS/code 0,`t_acquire_order.fail_code` 为空)。凡带 withhold=true 的用例(N102/N103/N106–N110)均因此失败。→ **"分账方代收手续费"功能在 UAT 未生效/未开通 或 缺陷**,待 dev/配置确认;非测试数据、非无分账能力(无 withhold 的 N101 完好)。

## 校验点(QA)
- 分账金额拆分正确(N101 已验:8 元分 4);分账退款 refundSharingAmount。
- 各分账方落账:[[tbl_acquireii_t_sharing_info]] `sharing_settled_amount` + `dpm.t_dpm_outer_account_subset` 余额;免登收银缓存卡支付路径。
- **withhold 分支**:`withholdAndRemitFee=True` 目前 UAT 下单即 FAILURE;回归前需 dev 确认该功能是否应生效(是→缺陷;否→用例应改为负例期望)。
- **回归缺口**:N103/N109 已补数据(cgs 本地 `test_data_uat.yml`,待推);带 withhold 的用例待 withhold 行为澄清后再判成功/负例。

## 来源与置信
- **UAT 实跑 2026-07-03/04**:N101(无 withhold)PASSED = 分账成功链路实测;N102(同数据 + withhold=True)= FAILURE(决定性对照);N103 补数据后仍 FAILURE(因 party1 withhold=True)。结论:分账能力正常,`withholdAndRemitFee=True` 行为待 dev 确认。
