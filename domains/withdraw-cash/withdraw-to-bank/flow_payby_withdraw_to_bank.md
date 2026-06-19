---
id: flow_payby_withdraw_to_bank
object_type: Flow
domain: withdraw-cash
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:PCW/1972174889
tags:
- withdraw
- iban
- fundout
- cashdesk
- h2h
subdomain: withdraw-to-bank
module: null
sensitivity: normal
name: 提现到银行卡端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Transfer to Bank Account（Transfer to your Bank）功能用于用户将余额账户的资金转入至银行卡账户。业务双方为用户与银行，资金走向会离开 PayBy 体系。本流程涵盖用户从提现页面提交订单，到银行返回成功/失败/退票的完整资金与状态流转，技术链路上分为 Place Order 与 Pay 两个阶段，跨 app-sdk / cgs / personal / fundout / cashdesk-api / pfs-payment / payment / cmf / cmf-task / h2h / BANK 多系统协作。

## 步骤(跨系统)

### 业务侧步骤
1. **入口进入**：用户从 wallet-withdraw-Transfer to Bank Account 或 home-Transfer-Transfer to Bank Account 进入。
   - Nokyc 用户进入会自动跳转实名认证页面。
   - KYC 用户：Account holder name 默认填写实名认证 name，不可编辑。
   - VIP 用户：Account holder name 默认为空，可编辑。
2. **填写提现信息**：在提现页面录入 Account name、IBAN、Amount(AED)；Bank name 通过接口由 IBAN 解析返回；也可从 Select Bank Account 页面点选已绑定卡直接带入（holder name、IBAN、Bank name 均不可编辑）。
3. **进入收银台**：Order Info 显示 Transfer to Bank Account，金额为 Amount+Fee，Payment Method 仅能使用余额。
4. **风控核身**：
   - 老版本：500 AED 以上出 OTP 验证，500 AED 以内仅验证密码。
   - 新版本接入风控核身后，由风控给出具体验证项。
5. **提交提现**：账单状态变为 Processing，用户收到通知 Processing。结果页每 10 秒定时轮询一次，成功/失败状态停止轮询。页面状态依次：提现提交 → 提现已提交至银行渠道。
6. **银行返回成功**：账单更新为 Transaction complete，用户收到 Success 通知；若使用新卡，提现成功时自动绑定该卡，将提交时的 holder name 保存为该提现卡的 Bank_Account_Name。
7. **银行返回失败**：账单更新为 Transfer Failed，用户收到 Transfer Failed 通知；资金原路退款，无退款订单。
8. **退票**：在银行成功后发生退票，账单更新为 Declined by Your Bank，无通知。

### Step 1: Place Order（技术时序）
1. Customer → app-sdk：发起提现。
2. app-sdk → cgs：`/personal/transfer/bank/submit`。
3. cgs → personal。
4. personal → fundout：`CashierFundoutFacade#createCashierFundout`。
5. fundout → cashdesk-api：`TokenServiceFacade#getFundoutToken`。
6. cashdesk-api → fundout → personal → cgs → app-sdk：返回 cashierUrl。
7. app-sdk → cgs：`/cashdesk/unityInitPayPage`。
8. cgs → cashdesk-api → cgs → app-sdk → Customer：进入收银台页面。

### Step 2: Pay（技术时序）
**Pay - Auth**
1. Customer → app-sdk → cgs：`/cashdesk/fundoutAuth`。
2. cgs → cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`。

**Pay - Verify**
3. Customer → app-sdk：身份验证（Verify identity）。
4. app-sdk → cgs：`/cashdesk/verify`。
5. cgs → cashdesk-api。
6. cashdesk-api → cmf：`CardTokenFacade#create`。
7. cashdesk-api → fundout：`FundoutSimpleFacade#pay`。
8. fundout → pfs-payment：`FundOutPaymentFacade#pay`。
9. pfs-payment → payment：`PaymentFacade#pay`。
10. payment → cmf：`FundRequestFacade#apply`。

**Batch Request Job**
11. Timer → cmf-task → h2h → BANK：批量发起提现请求。

**Batch Query Job**
12. Timer → cmf-task → h2h → BANK：批量查询结果。
13. cmf-task →> payment →> pfs-payment →> fundout：异步回写支付与提现状态。

## 涉及服务/表
- **服务**：app-sdk、cgs、personal、fundout、cashdesk-api、pfs-payment、payment、cmf、cmf-task、h2h、grc-check-identity-provider、BANK。
- **关键 Facade/接口**：
  - `/personal/transfer/bank/submit`、`/cashdesk/unityInitPayPage`
  - `/cashdesk/fundoutAuth`、`/cashdesk/verify`
  - `CashierFundoutFacade#createCashierFundout`
  - `TokenServiceFacade#getFundoutToken`
  - `PaymentSessionQueryStub#paymentSessionQuery`
  - `CardTokenFacade#create`
  - `FundoutSimpleFacade#pay`
  - `FundOutPaymentFacade#pay`
  - `PaymentFacade#pay`
  - `FundRequestFacade#apply`
- **业务数据**：wallet-cards 中提现卡列表（含 Bank_Account_Name，由提现成功时 holder name 写入）；账单 History（按月分组，安卓改为对接 H5 账单）。
- **测试链路**：basis 查询 payment order、支付控制立即结算、counter 管理置结果、审核订单。

## 校验点
- **Account name**：最大 30 字符；空格视为空值，无值文案 "Please enter holder name"；KYC 不可编辑、VIP 可编辑。
- **IBAN**：仅英文和数字；最大 32 位；前端规则 AE+21 位数字，校验失败提示 "Please enter a valid IBAN number."；前端通过后离开文本框时调接口校验。
- **Bank name**：不可编辑，IBAN 接口校验成功展示返回的 Bank name；失败 toast "Something went wrong. Please check and re-enter your IBAN number."。
- **Amount(AED)**：仅数字与小数点，最大 10 位、小数点后最多 2 位；超过 balance 时点击 next，iOS 文本框下方红字 "The amount you entered exceeds your available balance."，Android 文本变红并同文案；输入 0/0.0/0.00 视为空，iOS 红字 "Please enter a vaild amount."，Android toast 同文案。
- **Balance**：进入页面时获取当前 AED 余额；Transfer All 将 balance 录入 Amount。
- **限额限次**：K
