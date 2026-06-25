---
id: flow_unionpay_card_activation
object_type: Flow
name: UnionPay 银联卡激活端到端流程
aliases:
- unionpay-card-activation
- 银联卡激活
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268580390
tags:
- unionpay
- 激活
- 合规
- upic
related_services:
- svc_upic
related_tables: []
related_scenarios:
- scn_unionpay_usage
---

# UnionPay 银联卡激活端到端流程

## 概述
出于合规要求,用户在实际使用 UnionPay 功能前必须先**激活**。激活是用户可见流程:用户在激活页面勾选同意协议、点击激活按钮后完成激活,随后跳转进入 UnionPay 页面。激活可由 Money 页面入口、付款码入口、扫商户码入口等多个场景触发(各入口行为差异见 [[scn_unionpay_usage]])。区别于无感知的开卡(见 [[flow_unionpay_card_issuance]])。

## 步骤(跨系统)
1. 前置条件:用户已完成 KYC,且 [[svc_upic]] 已为用户开通银联卡(`upic.t_upi_card` 状态 `OS`)。
2. 用户从入口进入激活页面:
   - **Money 页面入口**:已 KYC 未激活用户点击入口,引导进入激活页面。
   - **付款码入口**:已 KYC 未激活用户在付款码 Tab 切到银联付款码时,显示"激活"按钮,点击进入激活流程。
   - **扫商户码入口**:已 KYC 未激活用户扫码后进入激活流程。
3. 激活页面展示:用户需勾选"同意协议"选框。
4. 用户点击激活按钮 → 完成激活。
5. 激活成功后跳转:
   - Money 入口:跳转至 UnionPay 页面(设置/修改 PIN、查看银联卡信息,安卓可开通 NFC)。
   - 付款码入口:回到付款码页面,展示银联付款码。
   - 扫商户码入口:进入下单页面(商户信息、金额输入框、Pay 按钮)。

## 关联关系
- **经过的服务(有序)**:[[svc_upic]](激活相关流程与银联卡数据;= `related_services`)
- **外部接口**:银联接口(合规与激活协议处理,外部,待补 svc 对象)
- **关键表**:`upic.t_upi_card`(银联卡记录,状态 `OS`;待补 tbl 对象)
- **关键场景**:[[scn_unionpay_usage]](= `related_scenarios`)

## 校验点
- 用户必须已完成 KYC(未 KYC 用户在 Money 入口直接报错;扫商户码入口引导去做 KYC)。
- 用户必须已开卡(`upic.t_upi_card` 状态 `OS`)。
- 激活页面必须勾选"同意协议"方可点击激活按钮(合规要求)。
- 激活流程必须合规执行,是用户可见流程(区别于无感知的开卡)。
- 激活完成后才允许使用 UnionPay 功能:展示银联付款码、扫商户码下单支付、NFC 刷卡等。
