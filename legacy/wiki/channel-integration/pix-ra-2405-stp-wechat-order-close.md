---
title: PIX RA-2405 STP微信渠道订单关闭流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-order-close
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:39fbfdea-c0ae-4ee3-be45-26ce0dbe6f18
tags: []
---

# PIX RA-2405 STP微信渠道订单关闭流程

本页描述海外钱包（Overseas wallet）在收到订单关闭请求后，与商户（Merchant）之间的订单关闭交互流程，以及五种处理结果分支对应的 `epcc.318.001.01` 回执报文字段组合。

## 流程概览

- 触发：海外钱包接收到上游支付相关消息（`..._E_PAYMENT`），进入 "Order processing is closed" 处理状态。
- 响应：海外钱包根据钱包侧订单状态与关闭处理结果，向商户回发 `Order closing receipt message [epcc.318.001.01]`。
- 差异化：通过回执报文中的 `OriSysRtnCd` 与 `OriBizStsCd` 字段组合区分不同结果分支。

## 结果分支与回执字段组合

五种互斥分支均使用同一回执报文类型 `epcc.318.001.01`：

1. **钱包正在支付且订单关闭成功** (wallet is paying and the order is closed successfully)
   - `OriSysRtnCd=00000000`
   - `OriBizStsCd=PB500034`

2. **钱包已支付成功，但订单关闭失败** (wallet payment was successful, but the order closing failed)
   - `OriSysRtnCd=00000000`
   - `OriBizStsCd=00000000`

3. **钱包支付失败，订单关闭失败** (wallet payment failed, order closing failed)
   - `OriSysRtnCd` 与 `OriBizStsCd` 按失败处理的返回码填写

4. **钱包订单不存在** (wallet order does not exist)
   - `OriSysRtnCd=00000000`
   - `OriBizStsCd=PB530001`

5. **钱包处理异常** (wallet processing exception)
   - Handling exceptions and reporting errors（异常处理并报错）

## 关键说明

- 回执报文类型固定为 `epcc.318.001.01`。
- 各分支为互斥的钱包侧订单关闭结果状态。
- 区分依据：`OriSysRtnCd` 与 `OriBizStsCd` 的取值组合。
