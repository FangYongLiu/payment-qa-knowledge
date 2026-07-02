---
id: reference_merchant_portal_products
object_type: Reference
name: PayBy 商户控台收款产品与功能指南
aliases: [merchant portal products, smart code, invoice, paylink, tax invoice, vam, statements]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613'
tags: [merchant-portal, smart-code, invoice, paylink, tax-invoice, vam, statements, sign-in]
related_services: [svc_merchant, svc_invoice, svc_hive_merchant_console]
---

# PayBy 商户控台收款产品与功能指南

> PayBy Merchant Portal(`b.payby.com`)是商户运营一站式控台，面向小微商户、商超、电商运营者，提供 collection、order inquiry/download、funds management。本页汇总登录与各收款产品(Smart Code / Invoice / Paylink / Tax Invoice / VAM)及对账单功能。资金/授权类操作(提现/退款/加员工)见 [[scn_merchant_settlement_withdraw_auth]]。

## 登录
- 入口 `b.payby.com` 或扫码;首次登录须先设置密码。
- 三种方式:Sign in with OTP(手机号 + 6 位 SMS Code)、Sign in with password、Sign in by scanning QR code。
- 控台菜单:Home、Transaction(Fiat/Crypto)、Statements、Products(Product List / Smart Code / Invoice / Paylink)、Management(Merchant Management、Tax Invoice)、Settings(Settlement、Authorizations)。
- 收单端交易查询(`Transactions => Fiat` Transaction Records):类型 Tab Purchase/Refund/Withdrawal/Cashback/Transfer/Transfer To Bank Account/Deposit;筛选 Date range(`dd-MM-yyyy HH:mm:ss ~ ...`)、(Merchant) Order No.、Subject、Terminal。该组合是收单交易查询慢 SQL 优化的核心入口。

## 产品申请(Product Application)
- 路径:`[Products] → [Product List] → [Lean More] → [APPLY NOW]`。
- 审核时长:1-2 working days;结果在 Portal 查看，审核完成发 SMS 通知。
- 可申请:Smart Code、Invoice、Paylink、VAM 等。

## Smart Code(店内贴码收款)
- 门店摆放一张二维码即可收款，无需硬件;顾客扫码支付，商户/指定员工即时收到通知。
- 新增:`[Products] → [Smart Code] → [Add New Code]`;详情页可下载/打印(示例码仅演示，勿用)。
- 添加 Follower 接收通知:`[Products] → [Smart Code] → [Manage] → [+ ADD FOLLOWER]` 选员工 → ENTER。

## Invoice(开票收款)
- 向客户手机/邮箱发账单，客户点击在线支付，支付成功商户收邮件通知。
- 创建:`[Products] – [Invoice] – [CREATE INVOICE]`。
- 字段:Customer name、Products information、Due date、客户联系方式、VAT(填 TRN 后可选 5%)、Discount、Title(Invoice/Bill/Tax Invoice)、Overdue rule(keep/cancel)。
- 操作:PREVIEW、SEND、SAVE AS INVOICE(定稿后不可编辑可后续 SEND)、SAVE AS DRAFT(可编辑)。

## Paylink(支付链接/按钮)
- 生成收款链接或嵌入按钮代码，放社媒/网页;顾客点开支付，成功后商户收邮件。
- 创建:`[Products] – [Paylink] – [ADD NEW]`(需先申请 Paylink 产品)。
- 配置:Paylink description、按钮样式、商品信息(可设顾客是否可改数量)、Logo(可选)。
- 列表可 Edit、复制 code(嵌入网页)/复制 link(发顾客)。

## Tax Invoice(PayBy 开给商户的税务发票)
- PayBy 按月向注册商户开具;`[Management] – [Tax Invoice]` 点下载图标查看/下载对应月份。
- 注意:与商户向客户开的 Invoice 不同。

## VAM(虚拟银行账户)
- 商户获专属 IBAN，打入该 IBAN 的资金**自动**划转至 PayBy 商户账户余额。
- 银行处理 VAM 激活通常需 1 个工作日;到账后与其他收款一并参与结算。
- 在产品申请中可申请 VAM。

## 对账单(Statements)
- 订阅每日汇总邮件:`[Statements] – [Subscribe]`，订阅后每日邮件发当日交易汇总。
- 下载:`[Statements]` → 选类型 → 选日期范围 → 搜索 → 下载。
- WPS 端移动端 Transactions(Tabs All/Incoming/Outgoing，按月筛选)右上 Download 进对账单下载弹层:`Download statement for AED 10.00`、Statement Duration(如 Last 6 Months)、Email(默认带出)、Request for a Hard Copy(勾选 +AED 26.50，必填 Shipping Address)、Confirm。

## ToC Add Funds(App 充值参考)
PayBy App ToC 用户 Add funds 页:确认金额(如 AED 1.00)→ 选可用支付方式(Apple Pay/Debit/Credit Card，不可用项 radio 禁用并附 `Unavailable for this service`)→ Pay;备选 Link your bank account / Add payment method / 右上 Deposit cash。

## 联系方式
- 商户支持:`merchant@payby.com`;银行账户变更走邮件流程(见 [[scn_merchant_settlement_withdraw_auth]])。
- 控台对应后端:[[svc_merchant]]、[[svc_invoice]]、[[svc_hive_merchant_console]];开放接口字段见 [[reference_payby_open_api]]。
