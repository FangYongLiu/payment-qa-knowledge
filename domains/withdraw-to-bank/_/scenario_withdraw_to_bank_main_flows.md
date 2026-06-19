---
id: scn_withdraw_to_bank_main_flows
object_type: Scenario
domain: withdraw-cash
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags:
- 提现
- 银行卡
- 场景
subdomain: null
module: null
sensitivity: normal
name: 提现到银行卡核心场景集
aliases:
- Transfer to Bank Account 核心场景
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account

## 前置条件
- Nokyc 用户进入转账自动跳转实名认证页面
- KYC 用户：Account holder name 默认填写实名认证 name，且不可编辑
- VIP 用户：Account holder name 默认为空，可编辑
- 仅可使用余额作为支付方式（收银台 Payment Method 限制）
- 限额限次：KYC 单日/单次 10K AED；VIP 无限制
- 费用：>10 AED 每笔收取 2 AED（2020/10/09 起）；≤10 AED 不收费
- 结算周期 T+1

## 操作步骤
**场景 1：提现提交**
1. 用户进入提现页面，输入 Account name、IBAN（前端校验 AED+21 位数字 → 离开文本框接口校验返回 Bank name）、Amount（AED）
2. 点击 next，进入收银台（Order Info 显示 Transfer to Bank Account，金额为 Amount+Fee）
3. 通过风控验证（旧版本：>500 OTP+密码，≤500 仅密码；新版本由风控给出验证项）
4. 提交成功 → 用户收到 Processing 通知，账单状态 Processing，结果页每 10 秒轮询一次

**场景 2：银行返回成功**
1. 提现已提交至银行渠道
2. 银行返回成功
3. 用户收到 Success 通知，账单更新为 Transaction complete
4. 自动绑定该提现卡，将提交时的 holder name 保存为该卡的 Bank_Account_Name

**场景 3：银行返回失败（原路退款）**
1. 银行返回失败
2. 用户收到 Transfer Failed 通知，账单更新为 Transfer Failed
3. 资金原路退款，无退款订单

**场景 4：银行成功后退票**
1. 银行成功后发生退票
2. 用户无通知
3. 账单状态更新为 Declined by Your Bank

## DB 校验点
- payment order 状态可在 basis 查询；测试环境走 mock 渠道时，可通过支付控制立即结算，counter 管理置结果后在审核订单中审核
- 提现成功后核对：提现卡绑定记录、Bank_Account_Name 是否保存为提交时的 holder name
- 失败场景核对：余额是否原路退回、是否无退款订单生成

## 预期结果
| 状态 | 通知 | 账单 |
|---|---|---|
| 提现提交 | Processing | Processing |
| 提现成功 | Success | Transaction complete |
| 提现失败 | Transfer Failed | Transfer Failed |
| 退票 | 无通知 | Declined by Your Bank |

- 结果页在成功/失败终态时停止轮询
- 失败场景余额原路退回且不产生退款订单
- 成功场景自动完成提现卡绑定
