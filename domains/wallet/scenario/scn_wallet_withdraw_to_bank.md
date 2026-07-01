---
id: scn_wallet_withdraw_to_bank
object_type: Scenario
name: 提现到银行卡场景 (Transfer to Bank Account 字段/状态/限额/测试)
aliases: [Transfer to Bank Account, payby-withdraw, withdraw-to-bank]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: wiki
source_ref: 'confluence:tester/124289192; wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7'
tags: [wallet, withdraw, iban, 提现, 限额, 费率, 校验]
related_services: [svc_cgs, svc_personal, svc_fundout, svc_cashdesk_api, svc_payment]
related_tables: []
related_logs: []
---

# 提现到银行卡场景 (Transfer to Bank Account)

> 业务测试场景:覆盖提现到银行卡的页面字段校验、用户身份差异、限额/费率/风控、四态状态流转与测试构造方法。端到端调用链见 [[flow_payby_withdraw_to_bank]]。

## 触发 / 入口
- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account
- 平台:iOS / Android。NoKYC 进入自动跳实名认证页。

## 关联关系
- **涉及服务**:[[svc_cgs]]、[[svc_personal]]、[[svc_fundout]]、[[svc_cashdesk_api]]、[[svc_payment]](= `related_services`)。
- **端到端流程**:[[flow_payby_withdraw_to_bank]]。
- **校验的表**:待补(toC 提现单物理表名原文未给)。
- **覆盖它的自动化**:[[auto_wallet_withdraw]] 覆盖 KYC/VIP/VVIP 提现回归(由 auto 的 `related_scenarios` 声明;本场景为字段/状态规则补充,二者互补)。

## 前置条件
- KYC 或 VIP 用户(字段编辑权限不同);测试环境渠道走 mock,不真实出款。

## 用户身份差异(Account holder name)
- **NoKYC**:进入转账自动跳实名认证。
- **KYC**:默认填实名 name,**不可编辑**;单日/单次支出限额各 10K AED。
- **VIP**:默认为空,**可编辑**;无限额。

## 操作步骤(页面字段校验)
1. **Account name**:最大 30 字符;空格视为空,无值文案 `Please enter holder name`;KYC 不可编辑、VIP 可编辑;超长 iOS 移动指针查看、Android 拖动查看。
2. **IBAN**:仅英文+数字,最大 32 位;前端规则 `AE+21 位数字`,失败红字 `Please enter a valid IBAN number.`;通过后离开文本框调接口二次校验。
3. **Bank name**:不可编辑,由 IBAN 接口校验返回;失败 toast `Something went wrong. Please check and re-enter your IBAN number.`。
4. **Amount(AED)**:仅数字+小数点,最大 10 位、小数后最多 2 位;超余额点 next:iOS 框下红字 / Android 文字变红,文案 `The amount you entered exceeds your available balance.`;输入 0/0.0/0.00 视为空,iOS 红字 / Android toast `Please enter a vaild amount.`(原文如此拼写)。
5. **Balance / Transfer All / View Price Plan**:进页取当前 AED 余额;Transfer All 一键填入全部余额;View Price Plan 进帮助中心看费率。
6. **Select Bank Account 选卡页**(入口 wallet → cards → 绑定提现卡):点已绑卡回填且三字段不可编辑;空列表显示 No Record;左滑删除(Confirm/Cancel);提现成功自动绑卡,holder name 存为 `Bank_Account_Name`。
7. **收银台**:Order Info=Transfer to Bank Account;金额=Amount+Fee;Payment Method 仅余额。

## 限额、费率、风控、结算
- **限额限次**:KYC 单日/单次各 10K AED;VIP 无限制。
- **费率历史**:2020/06/02 起 >50 AED 收 2 AED、≤50 不收;2020/10/09 起 >10 AED 收 2 AED、≤10 不收。
- **风控核身**:老版未接风控 >500 出 OTP、≤500 仅验密码;新版接风控由风控给出验证项。
- **结算周期**:2020/06/02 起 T+1。
- **渠道差异(View limit/方式选择)**:Aani(Recommended,Instant,费 AED 0.50)与 UAE bank(1-2 days,费 AED 2.00);选 UAE bank 显示 `Max withdraw amount = 余额 − 手续费`。

## DB 校验点 / 测试构造方法(mock 渠道)
1. APP 端按上述规则提交提现订单,账单/通知进入 Processing。
2. basis 查出对应 payment order,经"支付控制"立即结算。
3. counter 管理对订单**置结果**(成功/失败/退票)。
4. "审核订单"对置好的结果审核确认,状态正式落地。
- toC 提现单物理表名:待补。

## 预期结果(状态-通知-账单 映射)
| 状态 | 通知 | 账单 |
| --- | --- | --- |
| 提现提交 | Processing | Processing |
| 提现成功 | Success | Transaction complete |
| 提现失败 | Transfer Failed | Transfer Failed |
| 退票 | 无通知 | Declined by Your Bank |

- 结果页每 10 秒轮询一次,成功/失败终态停止;中间态:提现提交 → 已提交至银行渠道。
- 失败:资金原路退回,**无独立退款订单**。
- 退票:银行成功后发生,**不下发通知**,仅账单 `Declined by Your Bank`。
- 成功(新卡):自动绑卡,提交时 holder name 存为 `Bank_Account_Name`。
- 交易详情金额关系:`Amount(总扣款) = Receive Amount(到账) + Fees`;支付确认弹窗顶部大额=Amount+Fees,资金来源 Balance。

## 来源与置信
- 整合自归档 wiki(payby-withdraw / withdraw-to-bank 两套近重复文档 + 提现/选卡 UI 截图页 + 测试指南)。费率/版本为 2020 历史记录,**新版风控/H5 账单口径以现网为准(待复核)**。
