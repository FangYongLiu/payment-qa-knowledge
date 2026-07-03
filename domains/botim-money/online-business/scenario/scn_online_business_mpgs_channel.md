---
id: scn_online_business_mpgs_channel
object_type: Scenario
name: MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void)
aliases: [MPGS101-204, MPGS DirectPay, MPGS device pay, MPGS refund void]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: cgs-apitest
source_ref: cgs-apitest/testcases/payment/fundChannel/test_mpgs_fundIn_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, acquiring, MPGS, 3DS2, MOTO, DevicePay, 卡组织路由, 实测]
related_services: [svc_acquireii, svc_sgs, svc_qpay_mpgs, svc_tradeii, svc_cmf, svc_router]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_payment_info, tbl_acquireii_t_card_info, tbl_acquireii_t_refund_order, tbl_acquireii_t_void_order, tbl_cmf_tt_inst_order, tbl_cmf_tt_inst_order_result]
related_logs: []
---

# MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void)

> 业务测试场景:MPGS 渠道(MasterCard Payment Gateway Services)下 DirectPay 卡支付的全部受理形态,覆盖 MPGS101~204 子渠道路由。来源 cgs-apitest payment 套件。
> 所有用例经 SGS `acquire2/placeOrder` 下单,轮询 `acquire2/getOrder` 至 `PAID_SUCCESS`/`SETTLED`,核验 acquireii/tradeii/cmf 多库落库一致。

## 触发 / 入口
- 入口接口:[[api_sgs_acquire_place_order]],`paySceneCode=DIRECTPAY`(退款 TC023 用 `PAYPAGE`)。
- 查单/轮询:[[api_sgs_acquire_get_order]](`wait_for_order_success`);退款:[[api_sgs_acquire_refund_place_order]]。
- 商户密钥:`acs.t_key_config` 按 `PARTNER_ID` 取 `CERT_TYPE='PRIVATE'`、`enable_flag='Y'` 的 `RELATE_CERT` 作 `public_key`,对卡敏感数据 RSA 加密。

## 子场景与渠道分组(cgs-apitest 用例)
| 子场景 | 用例 | 渠道 / 行为 |
| --- | --- | --- |
| **DirectPay + 3DS2**(无 CVV) | TC001-004 `test_mpgs10x_3ds2_success` | MPGS101 Local MC / 102 Intl MC / 103 Local Visa / 104 Intl Visa |
| **MOTO 免 3DS 带 CVV** | TC005-008 `test_mpgs10x_cvv_moto_success` | MPGS105-108(Local/Intl × MC/Visa) |
| **MOTO 免 3DS 无 CVV** | TC009-012 `test_mpgs11x_NoCvv_moto_success` | MPGS109-112 |
| **设备支付**(MPGS131) | TC013-015 `test_mpgs131_{Apple/Google/Samsung}Pay_success` | INST_CODE = APPLEPAY/GOOGLEPAY/SAMSUNGPAY;免 3DS |
| 设备支付风控拒绝自动冲正 | TC016(**skip**,BUG-8393) | ApplePay 成功后风控拒绝触发 auto Reversal |
| **卡组织拆分路由** | TC017-020 `test_mpgs_cardOrgSplit_*` | PAYBY MC→MPGS101/102;NI VISA(Lottery)→MPGS202/204 |
| **退款 / AD Void** | TC021-023 | MPGS101 全额退款 / 部分退款 / PAYPAGE+cardToken AD 两阶段后 Void |

## 关联关系
- **涉及服务**:[[svc_sgs]]→[[svc_acquireii]]→[[svc_tradeii]]→[[svc_cmf]]→[[svc_qpay_mpgs]](MPGS 渠道)(= `related_services`)。
- **校验的表**:[[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_payment_info]]、[[tbl_acquireii_t_card_info]]、[[tbl_acquireii_t_refund_order]]、[[tbl_acquireii_t_void_order]];cmf 侧机构订单 [[tbl_cmf_tt_inst_order]](`FUND_CHANNEL_CODE`)与机构订单结果 [[tbl_cmf_tt_inst_order_result]](`API_RESULT_CODE`/3ds/cvv 扩展);`acs.t_key_config`(商户密钥)。

## 实测(UAT 2026-07-03,test_mpgs_fundIn)
**MPGS101 3DS2(MASTERCARD DC,商户 200000087655)**:DIRECTPAY product `200104` → `PAID_SUCCESS`;`channelParam.eciValue=02`、AuthCode/Stan/RRN、AcquireCode=00 Approved。落 [[tbl_cmf_tt_inst_order]] `FUND_CHANNEL_CODE=MPGS101`/`STATUS=S`;[[tbl_cmf_tt_inst_order_result]] `API_RESULT_CODE=CAPTURED`、`API_TYPE=VS`、EXTENSION `{3dsStatus:Y, eci:02, cvv_check:MATCH, 3dsVer:2.2.0, auth_code, authenticationStatus:CAPTURED}`。
**卡组织拆分 → MPGS202(NI VISA,商户 200000088683 "MPGS Card Org Split")**:同 DIRECTPAY,VISA CC(401200…0026)→ 路由到 **MPGS202**(NI 收单),`eciValue=05`(VISA);settlement 97.4 / payeeFee 2.73。

**★ 实测确认卡组织拆分路由**:同一下单接口,**按卡品牌路由到不同 MPGS 子渠道**——MASTERCARD→MPGS101/102(PAYBY),VISA→MPGS202/204(NI);ECI 也随品牌不同(MC=02 / VISA=05)。判定成功的机构侧口径:`tt_inst_order.STATUS=S` + `tt_inst_order_result.API_RESULT_CODE=CAPTURED`(API_TYPE=VS)。
- **测它的接口**:[[api_sgs_acquire_place_order]]、[[api_sgs_acquire_get_order]]、[[api_sgs_acquire_refund_place_order]](由各 API 的 `related_scenarios` 声明)。

## 前置条件
- 商户开通:Direct Pay Domestic Card、Direct Pay INTL Card(设备支付加 Auto Debit);TC019/020 商户为 Lottery 业务并配卡组织分流策略到 MPGS202/204。
- `acs.t_key_config` PRIVATE 证书可用;dpm 开通 AED 外部账户(退款用)。
- Fixtures:`self.sgs` / `self.mpgs_3ds`(`complete_3ds2_authentication`)/ `db_instance_factory('select'|'tradeii')` / `wait_for_order_success`;用例标 `@pytest.mark.uat`。

## 操作步骤(典型 3DS2 路径)
1. 用商户 PRIVATE 证书对卡四要素 RSA 加密,调 placeOrder(`paySceneCode=DIRECTPAY`,无 CVV)。
2. 断言同步 `status=CREATED`,取 orderNo/merchantOrderNo 与 `interActionParams.threeDSecureDom`。
3. 正则 `/3ds2/page/([A-Za-z0-9]+)` 提取 `threeDs_id`(未匹配抛 "3Ds not match");调 `mpgs_3ds.complete_3ds2_authentication(threeDs_id)`。
4. `wait_for_order_success(partnerId, orderNo, mode='SGS')` 轮询到 `PAID_SUCCESS`/`SETTLED`。
- **MOTO 路径(TC005-012)**:反向断言响应**不含** `threeDSecureDom`,不进 3DS2。
- **设备支付(TC013-015)**:带 `devicePayType`/`payCrypt`,免 3DS,不含 `threeDSecureDom`。
- **退款(TC021-023)**:支付成功后调退款下单,轮询退款单成功;TC023 PAYPAGE+cardToken 触发 AD(Authorize+Capture)后 Cancel/Void。

## DB 校验点
- `acquireii.t_acquire_order`:订单成功终态,`FUND_CHANNEL_CODE` 与用例对应(MPGS101~204/131)。
- `tradeii.t_trade_order`:`trade_status='SS'`。
- `cmf.tt_cmf_order` 主单 `STATUS='S'`;`cmf.tt_inst_order`/`tt_inst_order_result` 的 `FUND_CHANNEL_CODE`/`INST_CODE` 与用例渠道一致,结果成功。
- 退款:`t_refund_order` 生成且成功(TC022 退款额=原单 1/2,inst_order_result=`PARTIALLY_REFUNDED`);TC023 `t_void_order` 落库。

## 预期结果
- DirectPay 无 CVV → 返回 `threeDSecureDom`;MOTO → **不返回** `threeDSecureDom`;设备支付 → 免 3DS。
- FUND_CHANNEL_CODE 按卡类型(Local/Intl)、卡组织(MC/Visa)、是否带 CVV、卡组织分流策略正确路由到对应 MPGS 子渠道。
- acquireii→tradeii→cmf 三层订单/指令/结果数据一致。

## 来源与置信
- cgs-apitest payment MPGS 用例集整理;cmf 库表与 acs.t_key_config 对象待补。TC016 受 BUG-8393 阻塞为 skip。

> 测试卡:[[reference_mpgs_test_cards]] · [[reference_cko_test_cards]](卡支付/3DS/退款测试用官方测试卡)。
