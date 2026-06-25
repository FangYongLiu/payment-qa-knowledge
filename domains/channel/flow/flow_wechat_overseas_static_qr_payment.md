---
id: flow_wechat_overseas_static_qr_payment
object_type: Flow
name: 微信海外用户主扫静态码支付流程(EPCC)
aliases: [WeChat海外静态码, overseas static QR, EPCC scan]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: [wechat, overseas, static-qr, epcc, tenpayglobal, 海外扫码]
related_services: []
related_tables: []
related_scenarios: []
---

# 微信海外用户主扫静态码支付流程(EPCC)

## 概述
海外钱包用户使用钱包客户端主动扫描微信商户**静态二维码**完成支付。链路:Overseas wallet → TenpayGlobal → EPCC(清算/转接节点)→ WeChat Pay → Merchant backend。整体分三段:扫码识别(QR Scanning & Validation)、支付通知(Payment Notification)、支付结果校验(Payment Validation)。
注:与 pix MPC 接入(svc_pix)的关系待补;本流程为海外钱包侧 EPCC 报文链路。

## 步骤(跨系统)
### 阶段一:扫码与商户识别(User scans code)
1. User → Overseas wallet client:扫描 WeChat 商户二维码。
2. client → Overseas wallet:提交扫码结果。
3. Overseas wallet → TenpayGlobal:识别为 WeChat 码,调商户码查询 `QUERY_MERCHANT_CODE`。
4. TenpayGlobal → EPCC → WeChat Pay:查询商户订单 `epcc.305.001.01`。
5. WeChat Pay → EPCC → TenpayGlobal:商户订单回执 `epcc.306.001.01`。
6. TenpayGlobal → Overseas wallet → client → User:返回并展示商户详情(**此阶段不含订单信息**)。

### 阶段二:支付通知(Payment)
- User → client:输入金额并确认支付;client → Overseas wallet 提交支付请求,继续向 TenpayGlobal 侧发起后续支付。
- 待补:原文该阶段时序在 "Overseas wallet → Tenpay" 处截断,后续报文/回执以原始资料为准。

### 阶段三:支付结果校验(Payment Validation)
- 对应 "Payment result synchronization" 帧,用于支付结果同步与校验。待补:原文细节未给出。

## 关联关系
- **经过的服务(有序)**:Overseas wallet → TenpayGlobal → EPCC → WeChat Pay → Merchant backend(服务对象待补)
- **关键场景 / 参考**:[[scn_pix_wechat_vendor_api]]

## 关键报文与接口
- `QUERY_MERCHANT_CODE`:海外钱包向 TenpayGlobal 发起的商户码查询。
- `epcc.305.001.01`:商户订单查询请求(TenpayGlobal ↔ EPCC ↔ WeChat Pay)。
- `epcc.306.001.01`:商户订单查询回执。

## 校验点(订单关闭分支)
订单关闭场景海外钱包向商户回发 `Order closing receipt message epcc.318.001.01`,通过 `OriSysRtnCd` 与 `OriBizStsCd` 字段组合区分五种互斥结果:
1. 钱包正在支付且订单关闭成功:`OriSysRtnCd=00000000`,`OriBizStsCd=PB500034`。
2. 钱包已支付成功但订单关闭失败:`OriSysRtnCd=00000000`,`OriBizStsCd=00000000`。
3. 钱包支付失败、订单关闭失败:按失败处理的返回码填写。
4. 钱包订单不存在:`OriSysRtnCd=00000000`,`OriBizStsCd=PB530001`。
5. 钱包处理异常:异常处理并报错。
> 回执报文类型固定 `epcc.318.001.01`;区分依据为上述两字段组合。
