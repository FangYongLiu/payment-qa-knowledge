---
id: scn_payby_withdraw_core_cases
object_type: Scenario
domain: withdraw-cash
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289192
tags:
- 提现
- 测试场景
- 账单
- 通知
subdomain: null
module: null
sensitivity: normal
name: 提现核心测试场景集
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- wallet-withdraw-Transfer to Bank Account
- home-Transfer-Transfer to Bank Account

## 前置条件
- 用户已完成 KYC 或 VIP 实名认证（Nokyc 进入转账会自动跳转实名认证页面）
- 用户余额账户有 AED 余额可用
- 提现页面字段录入合法：Account name、IBAN（AE+21位数字，接口校验通过）、Bank name（接口返回）、Amount（合法且不超过 Balance）
- 测试环境走 mock 渠道：APP 提交提现订单后，通过 basis 查 payment order → 支付控制立即结算 → counter 管理置结果 → 审核订单审核结果

## 操作步骤
**场景1：提交提现**
1. 用户进入提现页面，输入 Account name、IBAN、Amount
2. 收银台展示 Order Info=Transfer to Bank Account、Amount+Fee、Payment Method 仅余额
3. 通过风控验证（老版本：>500 AED 走 OTP，≤500 AED 仅密码；新版本由风控给出具体验证项）
4. 提交提现订单

**场景2：银行返回成功**
1. 在场景1基础上，counter 置结果为成功并审核通过

**场景3：银行返回失败（原路退款）**
1. 在场景1基础上，counter 置结果为失败并审核通过

**场景4：银行成功后退票**
1. 在场景2基础上，触发退票

## DB 校验点
- payment order 已生成（可通过 basis 查询）
- 提现成功时自动绑定该卡，将提交时的 holder name 保存为该提现卡的 Bank_Account_Name
- 失败场景：原路退款，无退款订单
- 退票场景：账单状态更新为 Declined by Your Bank

## 预期结果
| 场景 | 通知 | 账单 |
|---|---|---|
| 提现提交 | Processing | Processing |
| 提现成功 | Success | Transaction complete |
| 提现失败 | Transfer Failed | Transfer Failed |
| 退票 | 无通知 | Declined by Your Bank |

补充：
- 结果页每 10 秒定时轮询一次，成功/失败状态不再轮询
- 提现失败原路退款，无退款订单
- 提现成功自动绑定该提现卡，holder name 保存为 Bank_Account_Name
- 限额：KYC 单日/单次支出 10K AED；VIP 无限制
- 费率（2020/10/09 起）：>10 AED 每笔收取 2 AED，≤10 AED 不收费
- 结算周期：T+1
