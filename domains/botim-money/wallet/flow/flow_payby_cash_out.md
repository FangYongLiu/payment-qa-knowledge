---
id: flow_payby_cash_out
object_type: Flow
name: 现金提现端到端流程 (Cash Out / Withdraw Cash via POS)
aliases: [PayBy Cash Out, Withdraw Cash, 现金提现, cashdesk fundout]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: wiki
source_ref: 'confluence:tester/124289136; wiki_image(cashdesk-fundout-sequence)'
tags: [wallet, cashout, cashdesk, fundout, pos, 现金提现]
related_services: [svc_cgs, svc_cashdesk_api, svc_grc_check_identity_provider, svc_fundout, svc_pfs_payment, svc_payment, svc_cmf, svc_cmf_task, svc_h2h]
related_tables: []
related_scenarios: []
---

# 现金提现端到端流程 (Cash Out / Withdraw Cash via POS)

## 概述
Cash Out(Withdraw Cash)允许用户将 PayBy 钱包余额**直接提取为现金**(而非进入银行卡),资金不走银行卡渠道。用户通过线下商户的 POS 机完成:出示付款码 → POS 扫码 → 用户核身 → 商户确认并付现 → 交易完成。系统侧由 Cashdesk 出款链路承载,经 fundout/pfs-payment/payment,最终在 cmf 落地为 FundRequest,由 cmf-task 批量对接 h2h 下发 BANK。提现入口与"提现到银行卡"并列展示于 Withdraw 页(见 [[flow_payby_withdraw_to_bank]])。

## 步骤(跨系统)

### 线下交互
1. 用户在 PayBy 端生成并出示付款码。
2. 商户用 POS 机扫描付款码。
3. 对用户身份进行核验。
4. 商户确认交易信息,将等额现金交付用户。
5. 交易完成。

### 系统侧调用链(Cashdesk 出款时序)
1. Customer → app-sdk → [[svc_cgs]]:`/cashdesk/fundoutAuth`。
   - cgs → [[svc_cashdesk_api]] → [[svc_grc_check_identity_provider]]:`PaymentSessionQueryStub#paymentSessionQuery`。
2. app-sdk → [[svc_cgs]]:`/cashdesk/verify`。
   - cgs → [[svc_cashdesk_api]],依次触发:
     - cashdesk-api → [[svc_cmf]]:`CardTokenFacade#create`(创建 CardToken)。
     - cashdesk-api → [[svc_fundout]]:`FundoutSimpleFacade#pay`。
       - fundout → [[svc_pfs_payment]]:`FundOutPaymentFacade#pay`。
       - pfs-payment → [[svc_payment]]:`PaymentFacade#pay`。
       - payment → [[svc_cmf]]:`FundRequestFacade#apply`。
3. app-sdk ⇠ Customer:同步返回 `apply success`。

### 异步批处理(Timer 驱动)
- **batch request job**:Timer → [[svc_cmf_task]] → [[svc_h2h]] → BANK,累积出款请求批量提交银行。
- **batch query job**:Timer → cmf-task,定期查询批次/交易状态并回流。

## 关联关系
- **经过的服务(有序)**:[[svc_cgs]] → [[svc_cashdesk_api]] → [[svc_grc_check_identity_provider]] → [[svc_cmf]] → [[svc_fundout]] → [[svc_pfs_payment]] → [[svc_payment]] → [[svc_cmf_task]] → [[svc_h2h]](= `related_services`)。app-sdk 与 BANK 为端点,无独立对象(待补)。
- **关键表**:待补(原文未提供物理表名)。
- **相关流程**:并列入口的"提现到银行卡"见 [[flow_payby_withdraw_to_bank]]。

## 校验点
- 付款码有效性(POS 扫码识别)。
- 身份核验:grc-check-identity-provider 经 `paymentSessionQuery` 通过。
- CardToken 创建:`CardTokenFacade#create` 成功。
- 出款申请链逐层成功:`FundoutSimpleFacade#pay` → `FundOutPaymentFacade#pay` → `PaymentFacade#pay` → `FundRequestFacade#apply`,返回 `apply success`。
- 商户确认后将现金交付用户。
- 批次任务:cmf-task 的 request job 与 query job 正常运行,确保 h2h 与 BANK 下发与回查闭环。
- 用户侧同步只收 `apply success`,真正出款由 cmf-task 异步推进。
