---
id: flow_payby_withdraw_to_bank
object_type: Flow
domain: payby-withdraw
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289192
tags:
- 提现
- 银行卡
- 资金流转
subdomain: null
module: null
sensitivity: normal
name: 提现到银行卡端到端流程
aliases:
- Transfer to Bank Account
- Transfer to your Bank
related_services: []
related_tables: []
related_scenarios:
- scn_payby_withdraw_core_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Transfer to Bank Account（Transfer to your Bank）功能用于用户将余额账户的资金转入至银行卡账户。业务双方为用户与银行，资金走向会离开 PayBy 体系。本流程涵盖用户从提现页面提交订单，到银行返回成功/失败/退票的完整资金与状态流转。

## 步骤(跨系统)
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

## 涉及服务/表
- 提现卡管理：wallet-cards 中的提现卡列表，字段 Bank_Account_Name（提现成功时由 holder name 写入）。
- 账单 History：按月分组，安卓后改为对接 H5 账单。
- 测试链路涉及：basis(查询 payment order)、支付控制(立即结算)、counter 管理(置结果)、审核订单。

## 校验点
- **Account name**：最大 30 字符；空格视为空值，无值文案 "Please enter holder name"；KYC 不可编辑、VIP 可编辑。
- **IBAN**：仅英文和数字；最大 32 位；前端规则 AE+21 位数字，校验失败提示 "Please enter a valid IBAN number."；前端通过后离开文本框时调接口校验。
- **Bank name**：不可编辑，IBAN 接口校验成功展示返回的 Bank name；失败 toast "Something went wrong. Please check and re-enter your IBAN number."。
- **Amount(AED)**：仅数字与小数点，最大 10 位、小数点后最多 2 位；超过 balance 时点击 next，iOS 文本框下方红字 "The amount you entered exceeds your available balance."，Android 文本变红并同文案；输入 0/0.0/0.00 视为空，iOS 红字 "Please enter a vaild amount."，Android toast 同文案。
- **Balance**：进入页面时获取当前 AED 余额；Transfer All 将 balance 录入 Amount。
- **限额限次**：KYC 单日 10K AED、单次 10K AED；VIP 无限制。
- **费率**（2020/10/09 起）：>10 AED 每笔收取 2 AED 费用，≤10 AED 不收费；历史规则（2020/06/02）为 >50 AED 每笔 2 AED，≤50 AED 不收费。
- **结算周期**：T+1。
- **状态-通知-账单一致性**：
  - 提现提交：通知 Processing / 账单 Processing
  - 提现成功：通知 Success / 账单 Transaction complete
  - 提现失败：通知 Transfer Failed / 账单 Transfer Failed
  - 退票：无通知 / 账单 Declined by Your Bank
- **轮询**：结果页每 10 秒一次，成功/失败状态停止轮询。
- **退款**：银行返回失败时原路退款，无退款订单。
