---
id: flow_payby_withdraw_to_bank
object_type: Flow
name: 提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani)
aliases: [Transfer to Bank Account, Transfer to your Bank, withdraw-to-iban, withdraw-to-aani]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: wiki
source_ref: 'confluence:PCW/1972174889; confluence:tester/124289192; wiki_image(cashdesk-fundout / toc-withdraw-add-funds-sequence)'
tags: [wallet, withdraw, iban, aani, fundout, cashdesk, 提现]
related_services: [svc_cgs, svc_personal, svc_fundout, svc_cashdesk_api, svc_grc_check_identity_provider, svc_pfs_payment, svc_payment, svc_cmf, svc_cmf_task, svc_h2h]
related_tables: []
related_scenarios: [scn_wallet_withdraw_to_bank]
---

# 提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani)

## 概述
Transfer to Bank Account（旧称 Transfer to your Bank）功能将用户的 PayBy 余额账户资金转出至 UAE 本地银行账户。业务双方为用户与银行,资金最终**离开 PayBy 体系**。技术链路分为 **Place Order(下单)** 与 **Pay(支付)** 两个阶段,Pay 再细分为 Auth / Verify / Batch Request Job / Batch Query Job,跨 app-sdk(无独立对象,待补)/ [[svc_cgs]] / [[svc_personal]] / [[svc_fundout]] / [[svc_cashdesk_api]] / [[svc_pfs_payment]] / [[svc_payment]] / [[svc_cmf]] / [[svc_cmf_task]] / [[svc_h2h]] 与银行(BANK,外部)多系统协作。提现渠道有 IBAN(UAE bank) 与 Aani 两种,后端链路一致,差异在到账时效与费率(见 [[scn_wallet_withdraw_to_bank]])。

## 步骤(跨系统)

### 业务侧
1. 入口:wallet → withdraw → Transfer to Bank Account,或 home → Transfer → Transfer to Bank Account(iOS/Android)。NoKYC 自动跳实名认证。
2. 填写 Account name / IBAN / Amount;Bank name 由 IBAN 调接口解析返回;也可从 Select Bank Account 选已绑卡直接带入(三字段不可编辑)。
3. 进入收银台:Order Info=Transfer to Bank Account,金额=Amount+Fee,Payment Method 仅余额。
4. 风控核身:老版本 >500 AED 出 OTP、≤500 仅验密码;新版接风控后由风控给出验证项。
5. 提交:账单/通知 Processing,结果页每 10 秒轮询,成功/失败终态停止轮询。
6. 结果:成功→账单 Transaction complete + 通知 Success(新卡成功时自动绑卡,holder name 存为 Bank_Account_Name);失败→账单/通知 Transfer Failed,原路退款无退款订单;退票→账单 Declined by Your Bank,无通知。

### Step 1: Place Order(技术时序)
1. Customer → app-sdk → [[svc_cgs]]:`/personal/transfer/bank/submit`。
2. cgs → [[svc_personal]]。
3. personal → [[svc_fundout]]:`CashierFundoutFacade#createCashierFundout`。
4. fundout → [[svc_cashdesk_api]]:`TokenServiceFacade#getFundoutToken`。
5. 逐层返回 fundout → personal → cgs → app-sdk:返回 `cashierUrl`。
6. app-sdk → cgs:`/cashdesk/unityInitPayPage`;cgs → cashdesk-api → 逐层返回,渲染收银台。

### Step 2: Pay - Auth
1. Customer → app-sdk → [[svc_cgs]]:`/cashdesk/fundoutAuth`。
2. cgs → [[svc_cashdesk_api]] → [[svc_grc_check_identity_provider]]:`PaymentSessionQueryStub#paymentSessionQuery`(风控返回需校验项)。

### Step 2: Pay - Verify
1. app-sdk 完成 `Verify identity` 后 → [[svc_cgs]]:`/cashdesk/verify`。
2. cgs → [[svc_cashdesk_api]]。
3. cashdesk-api → [[svc_cmf]]:`CardTokenFacade#create`(创建 CardToken)。
4. cashdesk-api → [[svc_fundout]]:`FundoutSimpleFacade#pay`。
5. fundout → [[svc_pfs_payment]]:`FundOutPaymentFacade#pay`。
6. pfs-payment → [[svc_payment]]:`PaymentFacade#pay`。
7. payment → [[svc_cmf]]:`FundRequestFacade#apply`(落地为 FundRequest)。用户侧同步仅收到 `apply success`。

### Batch Request Job / Batch Query Job(异步,Timer 驱动)
1. Timer → [[svc_cmf_task]] → [[svc_h2h]] → BANK:批量向银行发起出款请求。
2. Timer → cmf-task → h2h → BANK:批量查询银行结果。
3. cmf-task ⇢ [[svc_payment]] ⇢ [[svc_pfs_payment]] ⇢ [[svc_fundout]]:异步回写支付/提现/账单状态,作为成功/失败/退票最终来源。

## 关联关系
- **经过的服务(有序)**:[[svc_cgs]] → [[svc_personal]] → [[svc_fundout]] → [[svc_cashdesk_api]] → [[svc_grc_check_identity_provider]] → [[svc_pfs_payment]] → [[svc_payment]] → [[svc_cmf]] → [[svc_cmf_task]] → [[svc_h2h]](= `related_services`)。app-sdk 与 BANK 为端点,无独立对象(待补)。
- **关键场景**:[[scn_wallet_withdraw_to_bank]](= `related_scenarios`)。
- **关键表**:待补(原文未提供 toC 提现单物理表名)。

## 校验点
- Place Order 必须由 fundout 经 `TokenServiceFacade#getFundoutToken` 取得 token,cgs 才能返回 `cashierUrl` 初始化收银台。
- Pay-Auth 由 cashdesk-api 调 grc-check-identity-provider `paymentSessionQuery` 决定核身项;Verify 须在 sdk 完成 `Verify identity` 后才继续。
- Verify 链路顺序:cashdesk-api → cmf(`CardTokenFacade#create`) → fundout(`FundoutSimpleFacade#pay`) → pfs-payment(`FundOutPaymentFacade#pay`) → payment(`PaymentFacade#pay`) → cmf(`FundRequestFacade#apply`)。
- 与银行实际交互在 Batch Job(非同步实时);Batch Query Job 结果异步回传 payment → pfs-payment → fundout,为最终状态来源。
- 资金落库/状态流转的 toC 提现单物理表名:待补。
