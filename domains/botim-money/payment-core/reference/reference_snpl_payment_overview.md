---
id: reference_snpl_payment_overview
object_type: Reference
name: SNPL（Send Now Pay Later）支付总览
aliases: [snpl-payment-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: wiki:3fdb580e-54e6-410d-95ef-e2b28e622760
tags: [payment-core, wiki-overview]
related_services: [svc_3ds2, svc_botim_snpl, svc_cashierii, svc_payment, svc_remittance]
related_tables: []
---


# SNPL（Send Now Pay Later）支付总览

SNPL 允许用户基于授信额度先行完成汇款，后续再进行分期或延迟还款，作为一种新增支付方式接入收银台与支付渠道。

## 功能定义

- 用户使用信用额度先行完成汇款
- 后续支持分期或延迟还款

## 汇款首页影响

- **全新用户**：根据 `t_popup_control` 数据判断条件，弹框推荐使用 SNPL
- **未选中受益人时**，对已开通 SNPL 的用户：
  - 展示 SNPL banner
  - 无待还：展示可用额度
  - 有待还：展示待还金额
  - 已逾期：展示逾期信息
- 数据来源：remittance 调用 SNPL 查询，由 `init` 接口返回

## 收银台影响

- 收银台新增 SNPL 支付方式
- 选择 SNPL 支付后跳转至 SNPL 进行操作，对支付而言等同于进入银行 3DS 页面
- 用户操作完成后，收银台直接轮询支付结果
- 实际接入方式：SNPL 作为一个支付渠道，与 payby 对接
- 用户在 SNPL 页面操作成功后，SNPL 向支付渠道侧发送支付成功，由支付渠道一路同步至交易系统成功

## 订单详情

- 使用 SNPL 支付的汇款订单，订单详情需展示 SNPL 支付方式

## 对渠道的影响

- 渠道侧一般不感知支付方式，仍然只认定到账
- SNPL 的核心逻辑发生在收银台与支付系统

## 风险控制

- 需结合风控 / 额度管理模块
