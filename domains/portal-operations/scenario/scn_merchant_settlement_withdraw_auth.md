---
id: scn_merchant_settlement_withdraw_auth
object_type: Scenario
name: 商户控台结算/提现/退款的双人授权
aliases: [settlement withdraw refund authorization, 提现授权, 退款授权]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613'
tags: [merchant-portal, settlement, withdraw, refund, authorization]
related_services: [svc_merchant, svc_statementii]
related_tables: []
related_logs: []
---

# 商户控台结算/提现/退款的双人授权

## 触发 / 入口
PayBy Merchant Portal(`b.payby.com`)中商户发起手动提现(Withdraw)、退款(Refund)或添加员工(Add Staff)等敏感操作，均需经管理员(admin)或财务(financial)账号授权后才生效。核心校验:**双人授权机制**。

## 关联关系
- **涉及服务**:[[svc_merchant]]、[[svc_statementii]](= `related_services`)
- **相关流程**:产品申请见 [[flow_acquire_product_application]];控台产品功能见 [[ref_merchant_portal_products]]
- **校验的表**:结算配置 `statementii.t_settlement_config`、提现 `mhtfundout.t_withdraw_order`(对象待补)

## 前置条件
- 商户已入驻并以 Payment 业务登录控台(见 [[flow_merchant_onboarding]])。
- 存在 admin 与/或 financial 角色账号用于授权。

## 操作步骤
### 结算设置(Settlement)
`[Settings] → [Settlement]`:配置自动结算开关、Cut-off time(到点后资金发往银行)、Daily Reserve amount(每日保留金额，用于退款等场景);修改需输入密码后 SUBMIT。

### 手动提现(Manually Withdraw)
1. `[Home] → [Withdraw]`，输入金额 → Next → 输入密码 → Confirm。
2. 授权:admin / financial 账号在 `[Settings] → [Authorizations] → [My Authorization] → [Authorize]` 完成。
3. 规则:financial staff 发起的提现，需 admin 或**另一个** financial 账号授权。

### 退款(Refund)
1. `[Transaction] → [Fiat]`，找到目标订单点击 [Refund] 提交退款请求。
2. 授权人(admin / financial)在 `[Settings] → [Authorizations]` 找到对应订单点击 [Refund] 完成授权。
3. 规则:financial staff 发起需 admin 或另一 financial 授权。

### 添加员工(Add Staff)
1. `[Management] → [Merchant Management] → [Staff Information] → [+ ADD STAFF]`。
2. 管理员在 `[Settings] → [Authorizations] → [My Authorization] → [Authorize]` 授权后生效。

### 添加/变更银行账户
不在控台自助办理，需邮件 `merchant@payby.com`，提供:盖章官方信函(含 PayBy MID、Account Holder Name 须与营业执照一致、IBAN、Beneficiary Address、Bank Name)+ Bank Letter/Statement(显示 Account Name 和 IBAN)。

## DB 校验点
- `statementii.t_settlement_config`:Reserved Amount / Minimum Withdrawal Amount 等结算参数。
- 提现/退款订单落库及状态流转表「待补」(关联 `mhtfundout.t_withdraw_order`、`acquireii.t_refund_order`)。

## 预期结果
- 未授权的提现/退款/加员工请求停留在待授权状态，不进入后续处理。
- 授权完成后提现进入后台结算流程;退款进入退款流程。
> 双人授权(发起人 ≠ 授权人)是该场景的核心校验点。
