---
id: flow_remittance_send_money
object_type: Flow
name: Send Money 端到端转账流程
aliases: [Send Money, Wallet Redesign Send Money]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/185794690; wiki:77b3f2a6-a8a3-4481-944a-58fb9f23fdda; wiki_image:9f0c0a0d-1a4b-4e72-b124-d44b671ddd00
tags: [send-money, transfer, kyc, refund, notification]
related_services: [svc_cashierii, svc_tradeii, svc_transfer, svc_pns]
related_tables: []
related_scenarios: [scn_remittance_send_money]
---

# Send Money 端到端转账流程

## 概述
Send Money 端到端转账流程:从付款人(Payer)在 Botim 消息窗发起转账,经收银台/交易系统扣款,到收款人(Payee)按 KYC 状态领取,以及订单过期触发退款的完整业务链路。
与手机号转账不同,Send Money 在付款人与收款人之间点对点结算(手机号转账经付款人中间户中转);收款人已 KYC 时走自动结算,未 KYC 时通过聊天气泡通知,KYC 完成后由系统自动结算领取。起点 = Payer 在消息窗发起 Send Money;终点 = 收款人领取到账或订单过期退款。

## 步骤(跨系统)
1. **Botim message window → Payer**:进入 Send Money(Enter send money),Payer 本地确认 Send。
2. **Payer → [[svc_cashierii]]**:Pay(发起收银台支付)。
3. **[[svc_cashierii]] → [[svc_tradeii]]**:Pay,tradeii 处理扣款。
4. **[[svc_tradeii]] → [[svc_transfer]]**:Notice payment result(转账核心 cgs/transfer 更新订单 Update order)。
   - 注:原 wiki 时序图中转账核心标为 `cgs/transfer`,此处归到 [[svc_transfer]];与 [[svc_cgs]] 网关的关系待补。
5. **[[svc_transfer]] → 通知**:更新订单后按收款人(Payee)状态进入三选一的通知分支:
   - **已注册并已 KYC(Registered with KYC)**:→ [[svc_pns]] 消息窗通知;Payee 收到 Received(已入账),自动结算到账。
   - **已注册但未 KYC(Registered without KYC)**:→ [[svc_pns]] 消息窗通知;Payee 收到 Receiving(待领取),KYC 完成后系统自动结算领取(仍可能失败)。
   - **未注册(Unregistered)**:→ mns(短信通知服务,**待补**:对象未建)发送 Sms notification;Payee 收到 Receive remind。
6. **订单过期 / 退款**:
   - 收款人未 KYC:72H 未领取触发退款,发送聊天气泡通知。
   - 收款人已 KYC:自动领取失败时 24H 退款;正常路径下只会出现支付失败。

## 关联关系
- **经过的服务(有序)**:[[svc_cashierii]] → [[svc_tradeii]] → [[svc_transfer]] → [[svc_pns]](= `related_services`,串起整条链;mns 短信服务对象待补)
- **关键表**:待补(原文数据库设计图未能下载解析:Send Money 订单 / 领取状态 / 退款记录等表)
- **关键场景**:[[scn_remittance_send_money]](= `related_scenarios`)

## 校验点
- 收款人 KYC 状态判定:决定走自动结算还是手动结算 / 待领取路径(已 KYC=自动,未 KYC=待领取)。
- 自动结算成功 / 失败判定:失败需进入 24H 退款流程(已 KYC 场景)。
- 订单过期时限:未 KYC 场景 72H 退款;已 KYC 自动领取失败 24H 退款。
- 通知通道与文案:已注册走 [[svc_pns]] 消息窗(已 KYC=Received / 未 KYC=Receiving),未注册走短信(mns)Receive remind;全程区别于手机号转账的公众号 + 短信通知。
- 资金路径:Send Money 点对点结算(对比手机号转账经付款人中间户中转)。
