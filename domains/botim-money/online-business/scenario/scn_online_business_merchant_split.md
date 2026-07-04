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

**先前"14 failed"根因 = cgs 测试数据缺口,非缺陷/非配置**:`data/payment/test_data_uat.yml` **只定义了 `test_merchantSplit_N101`**,而用例文件有 N101–N110 共 10 个 → N102–N110 因 `KeyError`(数据未定义)报错。**待补 cgs 侧**:补 N102–N110 的 test data(不同金额/多分账方/`withholdAndRemitFee`/分账退款等)。

## 校验点(QA)
- 分账金额拆分正确(N101 已验:8 元分 4);分账退款 refundSharingAmount。
- 各分账方落账:[[tbl_acquireii_t_sharing_info]] `sharing_settled_amount` + `dpm.t_dpm_outer_account_subset` 余额;免登收银缓存卡支付路径。
- **回归缺口**:N102–N110 需在 cgs `test_data_uat.yml` 补测试数据后才能覆盖(非产品问题)。

## 来源与置信
- **UAT 实跑 2026-07-03**(`test_merchant_split_fangyong.py::N101` PASSED):分账成功链路为实测;N102–N110 因 cgs 测试数据未定义(KeyError)未覆盖,与产品无关。
