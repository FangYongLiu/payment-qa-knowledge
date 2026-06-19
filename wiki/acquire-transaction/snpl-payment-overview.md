---
title: SNPL（Send Now Pay Later）支付业务说明
domain: acquire-transaction
kind: wiki_page
slug: snpl-payment-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268547812
tags: []
---

# SNPL（Send Now Pay Later）支付业务说明

SNPL 是一种基于信用额度的"先汇款、后还款"支付方式，用户可使用授信额度先完成汇款，再进行分期或延迟还款。

## 功能定义

- 全称：Send Now Pay Later
- 核心能力：用户使用信用额度先行完成汇款，后续分期或延迟还款

## 汇款首页展示逻辑

汇款首页对 SNPL 的露出分为弹框与 Banner 两类，相关数据由 remittance 调用 SNPL 查询后通过 init 接口返回。

### 弹框（全新用户推荐）
- 全新用户进入汇款首页会弹框推荐开通使用 SNPL
- 弹出条件依据 `t_popup_control` 表数据判断

### Banner（已开通用户）
未选中受益人、且已开通过 SNPL 的用户，会展示 SNPL Banner，根据账户状态展示不同内容：
- 没有待还：展示可用额度
- 有待还：展示待还金额
- 有逾期：展示逾期信息

## 收银台接入

- 收银台阶段新增 **SNPL 支付方式**
- 用户选择 SNPL 支付后，会跳转至 SNPL 页面进行操作
  - 对支付系统而言，等同于进入银行 3DS 页面
  - SNPL 操作完成返回后，收银台直接轮询支付结果
- 实现方式：SNPL 实际作为一个支付渠道，与 **PayBy** 对接
- 支付成功链路：
  1. 用户在 SNPL 页面操作成功
  2. SNPL 向支付渠道侧发送支付成功通知
  3. 支付渠道逐级同步至交易系统，标记成功

## 订单详情展示

- 若汇款订单使用 SNPL 支付，订单详情页需展示 SNPL 支付方式

## 对渠道的影响

- 渠道侧一般不感知具体支付方式，仍只认定到账
- SNPL 的业务逻辑主要发生在 **收银台** 与 **支付系统** 层面

## 风险控制

- 需结合风控 / 额度管理模块进行授信与风险评估
