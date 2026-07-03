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
source_ref: cgs-apitest/testcases/payment/toB/test_merchant_split_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测, 待核实]
related_services: [svc_acquireii, svc_tradeii, svc_payment, svc_pfs_payment, svc_merchant]
related_tables: [tbl_acquireii_t_sharing_info]
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

## ⚠️ 实测观察(UAT 2026-07-03,test_merchant_split —— 需核实,非结论)
本轮 `test_merchant_split` **多数用例未通过**:带 `sharingInfoList` 的 `placeOrder` 返回 `head` SUCCESS/code 0,但 `acquireOrder.status` 直接为 **`FAILURE`**(或停在 `CREATED` 不结算);另有部分 cgs 用例因**测试数据缺失**(`KeyError: test_merchantSplit_N10x`)未执行。**本次未取到干净的分账成功样本**——需核实是**子商户分账配置/测试数据**问题还是**缺陷**(商户 200000080798 → 分账方 200000087655)。分账成功链路的落库校验暂 **待补**(拿到成功样本后补 `t_sharing_info` 勾稽)。

## 校验点(QA)
- 分账金额拆分正确;分账退款 refundSharingAmount。
- 各分账方落账([[tbl_acquireii_t_sharing_info]]);免登收银缓存卡支付路径。
- **回归关注**:上述 UAT 分账下单 FAILURE 需先定位(配置/数据/缺陷)再断言成功链路。

## 来源与置信
- **UAT 实跑 2026-07-03**(`test_merchant_split_fangyong.py`,14 failed/多为分账态 FAILURE + 测试数据 KeyError):请求结构为实测;成功落库链路待取样。
