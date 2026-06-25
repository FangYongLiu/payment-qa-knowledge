---
id: flow_add_funds_via_bank_card
object_type: Flow
name: 银行卡充值(Add Funds via Bank Card)端到端流程
aliases:
- add-funds-via-bank-card
- 银行卡充值
- ToC Add Funds
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PCW/1412988949; wiki:30b14d13-f138-4933-9a9e-82e4ba95aaa6; wiki_image:a0228e99-6349-44e8-8d89-3c6754fc7afa; wiki_image:cfaf8167-d8cd-485b-9212-70b3441cab80
tags:
- add-funds
- deposit
- bank-card
- 3ds
- cashier
related_services:
- svc_cgs
- svc_personal
- svc_deposit
- svc_tradeii
- svc_cashierii
- svc_pfs_payment
- svc_payment
- svc_cmf
- svc_qpay_cko
- svc_fcw
related_tables: []
related_scenarios: []
---

# 银行卡充值(Add Funds via Bank Card)端到端流程

## 概述
用户通过银行卡向 PayBy 钱包充值(Add Funds / top-up)的端到端两阶段时序,覆盖从 app-sdk 提交到银行 3DS 校验及支付结果异步回调的完整主链路:

- **Step 1 · Place Order(下单)**:app-sdk 发起 submit deposit,经 [[svc_cgs]] → personal → [[svc_deposit]] → [[svc_tradeii]] → [[svc_cashierii]],生成 `cashierToken` 并初始化交易,返回 `tokenUrl` 给客户端。
- **Step 2 · Card Pay(卡支付)**:客户端发起 confirm-pay,经 [[svc_cashierii]] 完成支付会话查询、身份验证(verify)、创建卡 token,再走支付链路([[svc_tradeii]] → [[svc_pfs_payment]] → [[svc_payment]] → [[svc_cmf]] → qpay-cko → BANK);银行返回 3DS 表单由客户端完成验证,最后通过 fcw 异步回调结果。

> 范围说明:本流程仅覆盖主流程系统调用,**省略了查询类操作**:member 查询、merchant 查询、手续费(fee)计算、结算周期查询、商户支付方式鉴权查询、风控识别、渠道路由等。原文(Add Funds Overview)建议新系统设计图不要引入此类间接依赖系统。
>
> 业务范围补充:BOTIM Transfer 已迁移至 Transfer 业务域;Withdraw via IBAN 不属于本流程 scope。

## 步骤(跨系统)

### Step 1:Place Order(下单)
1. Customer → app-sdk:`submit deposit`
2. app-sdk → [[svc_cgs]]:`POST /personal/deposit/v1/auth/submit`
3. cgs → personal
4. personal → [[svc_deposit]]:`CashierDepositFacade#createCashierDeposit`
5. deposit → [[svc_tradeii]]:`CashierTradeFacade#createCashierTrade`
6. tradeii → [[svc_cashierii]]:`OrderTokenFacade#getTradeOrderToken`
7. cashierii → tradeii:返回 `cashierToken`
8. 逐层回传 tradeii → deposit → personal → cgs → app-sdk:得到 `tokenUrl`
9. app-sdk → [[svc_cgs]]:`POST /cashierii/order/v1/auth/init-trade`
10. cgs → [[svc_cashierii]] → cgs → app-sdk → Customer

### Step 2:Card Pay(卡支付)

#### Confirm Pay(确认支付)
1. Customer → app-sdk:submit deposit
2. app-sdk → [[svc_cgs]]:`POST /cashierii/pay/v1/auth/confirm-pay`
3. cgs → [[svc_cashierii]]
4. cashierii → grc-component-connect-provider:`PaymentSessionQueryStub#paymentSessionQuery`(支付会话查询)

#### Verify(身份验证)
5. Customer 在 sdk 内完成 verify identity
6. app-sdk → [[svc_cgs]]:`POST /cashierii/pay/v1/auth/verify`
7. cgs → [[svc_cashierii]]
8. cashierii → [[svc_cmf]]:`CardTokenFacade#create`(创建卡 token)
9. cashierii → [[svc_tradeii]]:`CashierTradePayFacade#confirmPay`
10. tradeii → [[svc_pfs_payment]]:`QuickPayPaymentFacade#pay`
11. pfs-payment → [[svc_payment]]:`PaymentFacade#pay`
12. payment → [[svc_cmf]]:`FundRequestFacade#apply`
13. cmf → qpay-cko([[svc_qpay_cko]]):`ChannelFundFacade#apply`
14. qpay-cko → BANK(发卡行)
15. app-sdk → Customer:返回 `3ds bank form`

#### 3DS Verification(3DS 验证)
16. Customer → BANK:发起并完成 3DS 验证

#### Pay Result Callback(支付结果异步回调)
17. BANK → [[svc_fcw]]:pay result
18. fcw → [[svc_cmf]]
19. cmf →> [[svc_payment]]
20. payment →> [[svc_pfs_payment]]
21. pfs-payment →> [[svc_tradeii]]
22. tradeii →> [[svc_deposit]](最终回写充值结果)

## 关联关系
- **经过的服务(有序)**:[[svc_cgs]] → [[svc_personal]] → [[svc_deposit]] → [[svc_tradeii]] → [[svc_cashierii]] → [[svc_pfs_payment]] → [[svc_payment]] → [[svc_cmf]] → [[svc_qpay_cko]] → [[svc_fcw]](= `related_services`)
- **外部参与方**:BANK(发卡行,外部)、grc-component-connect-provider(风控会话查询,跨域服务,待补 svc 对象)
- **关键表**:待补(原文未提供 deposit/trade/cashier 落库表结构)
- **关键场景**:待补

## 关键 Facade / HTTP 入口
- HTTP 入口:`/personal/deposit/v1/auth/submit`、`/cashierii/order/v1/auth/init-trade`、`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify`
- 关键 Facade:`CashierDepositFacade#createCashierDeposit`、`CashierTradeFacade#createCashierTrade`、`OrderTokenFacade#getTradeOrderToken`、`PaymentSessionQueryStub#paymentSessionQuery`、`CardTokenFacade#create`、`CashierTradePayFacade#confirmPay`、`QuickPayPaymentFacade#pay`、`PaymentFacade#pay`、`FundRequestFacade#apply`、`ChannelFundFacade#apply`

## 校验点
- **Place Order**:cashierii 通过 `OrderTokenFacade#getTradeOrderToken` 生成 `cashierToken`,最终返回 `tokenUrl` 作为支付入口;app-sdk 必须使用该 token 通过 cgs 调用 `init-trade`(cgs 在 init-trade 直接路由到 cashierii,跳过 personal/deposit/tradeii 中间链路)。
- **Confirm Pay**:cashierii 调用 `paymentSessionQuery` 查询支付会话。
- **Verify**:客户端在 sdk 内完成 verify identity 后,cashierii 通过 `CardTokenFacade#create` 创建卡 token。
- **3DS**:qpay-cko 调用 BANK 后,sdk 向客户端返回 `3ds bank form`;客户端必须直接与 BANK 完成 3DS 验证。
- **结果回调**:BANK → fcw → cmf → payment → pfs-payment → tradeii → deposit 采用异步回传,需保证各层结果正确传递并最终回写至 deposit。
- **充值页 UI(QA 已知点)**:App "Add funds" 页含余额展示、金额输入、快捷档位(100/200/500/1000)、View limit、Proceed to add funds CTA。**已知疑似缺陷**:余额币种显示为 `AED`,金额输入框币种符号显示为 `₿`(疑似 BHD 字形),二者不一致,需重点验证币种渲染逻辑与符号映射。
