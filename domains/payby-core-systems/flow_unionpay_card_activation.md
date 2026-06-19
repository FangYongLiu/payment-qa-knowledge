---
id: flow_unionpay_card_activation
object_type: Flow
domain: payby-core-systems
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1268580390
tags:
- UnionPay
- 激活
- 合规
subdomain: null
module: null
sensitivity: normal
name: UnionPay激活端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
由于合规要求，用户在实际使用 UnionPay 功能前必须先进行激活。激活是用户可见流程：用户在激活页面勾选同意协议、点击激活按钮后完成激活，随后跳转进入 UnionPay 页面。激活流程可由 Money 页面入口、付款码入口、扫商户码入口等多个场景触发。

## 步骤(跨系统)
1. 前置条件：用户已完成 KYC，且 upic 已为用户开通银联卡（记录在 upic.t_upi_card，状态为 OS）。
2. 用户从入口进入激活页面：
   - Money 页面入口：已 KYC 未激活用户点击入口，引导进入激活页面。
   - 付款码入口：已 KYC 未激活用户在付款码 Tab 切换到银联付款码时，显示"激活"按钮，点击进入激活流程。
   - 扫商户码入口：已 KYC 未激活用户扫码后进入激活流程。
3. 激活页面展示：用户需勾选同意协议的选框。
4. 用户点击激活按钮 → 完成激活。
5. 激活成功后跳转：
   - Money 入口场景：跳转至 UnionPay 页面（可设置/修改 PIN、查看银联卡信息，安卓手机可开通 NFC）。
   - 付款码入口场景：回到付款码页面，展示银联付款码。
   - 扫商户码入口场景：进入下单页面（商户信息、金额输入框、Pay 按钮）。

## 涉及服务/表
- upic 应用（接收激活相关流程，承载银联卡数据）
- upic.t_upi_card（银联卡记录表，状态 OS 表示已开卡）
- 银联接口（合规与激活相关协议处理）

## 校验点
- 用户必须已完成 KYC（未 KYC 用户在 Money 入口直接报错；扫商户码入口引导去做 KYC）。
- 用户必须已开卡（upic.t_upi_card 状态 OS）。
- 激活页面必须勾选"同意协议"选框，方可点击激活按钮（合规要求）。
- 激活流程必须合规执行，是用户可见流程（区别于无感知的开卡）。
- 激活完成后才允许使用 UnionPay 功能：展示银联付款码、扫商户码下单支付、NFC 刷卡等。
