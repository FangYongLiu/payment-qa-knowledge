---
id: scn_unionpay_usage
object_type: Scenario
name: UnionPay 三入口使用场景(Money / 付款码 / 扫商户码 + 外币)
aliases:
- unionpay-usage-scenarios
- 银联应用场景
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268580390; wiki:4e177d56-875e-413a-a120-94fb6aefb87b
tags:
- unionpay
- payment
- 付款码
- 外币
related_services:
- svc_upic
related_tables: []
related_logs: []
---

# UnionPay 三入口使用场景(Money / 付款码 / 扫商户码 + 外币)

## 触发 / 入口
UnionPay 功能在 App 内有三个入口:Money 页面、付款码、扫商户码。各入口行为按用户状态(未 KYC / 已 KYC 未激活 / 已激活)分流。开卡见 [[flow_unionpay_card_issuance]],激活见 [[flow_unionpay_card_activation]]。

## 关联关系
- **涉及服务**:[[svc_upic]](= `related_services`;所有 UnionPay 支付场景的资金落地由银联回调 upic 扣款接口完成)
- **校验的表**:`upic.t_upi_card`(开卡/状态;待补 tbl 对象)
- **相关日志**:待补
- **相关流程**:[[flow_unionpay_card_issuance]] / [[flow_unionpay_card_activation]]

## 通用前置状态(三入口统一)
- **未 KYC**:拒绝或引导去 KYC。
- **已 KYC 未激活**:引导进入激活页面,激活完成后回到原入口。
- **已激活**:进入正常功能。

## 入口与行为

### 1. Money 页面入口
- 未 KYC 用户:点击入口**直接报错**。
- 已 KYC 未激活:引导进入激活页面,激活成功后跳转至 UnionPay 页面。
- UnionPay 页面功能:设置/修改 PIN;查看银联卡信息;安卓手机提供开通 NFC 按钮,在支持银联的 POS 机刷卡时由银联调 upic 扣款接口,从用户钱包扣款。

### 2. 付款码入口
- 未 KYC 用户:付款码页面仅展示自有付款码。
- 已 KYC 用户:付款码页面带 Tab,可在自有付款码与银联付款码间切换。
  - 未激活:银联付款码不展示,显示"激活"按钮,点击进入激活流程;激活成功后回到付款码页面展示银联付款码。
  - 已激活:直接展示银联付款码,商户扫码即可完成支付(银联调 upic 扣款接口)。

### 3. 扫商户码入口
- 未 KYC 用户:扫码后引导去做 KYC。
- 已 KYC 未激活用户:扫码后进入激活流程。
- 已激活用户:扫码进入下单页面(我方页面),含商户信息、金额输入框、Pay 按钮。

## 外币场景特殊处理(扫商户码)
- 输入框展示**外币金额**,并显示"约等于 AED 金额"。
- 汇率来自数据库,**每日从银联官网同步**。
- 点击 Pay 呼起收银台,金额以 AED **预估值**展示。
- 提交支付时银联返回**真实的 AED 金额**,可能与收银台预估不同。
- 用户端流程在提交后即结束,因此**实际扣款金额与收银台展示金额可能存在差异**。

## DB 校验点
- `upic.t_upi_card`:开卡记录及状态(`OS` 已开卡);完整字段待补。

## 预期结果 / QA 关注点
- 三入口在三种用户状态下行为正确分流(报错 / 引导 KYC / 引导激活 / 正常功能)。
- 开卡过程对用户无感知,激活是用户可见流程,必须合规执行。
- **upic 扣款接口**是所有 UnionPay 支付场景(NFC 刷卡、付款码被扫、扫商户码支付)的资金落地关键。
- 外币支付:重点验证预估 AED 金额与实际扣款金额的差异提示与对账一致性。
