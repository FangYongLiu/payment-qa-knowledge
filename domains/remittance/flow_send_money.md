---
id: flow_send_money
object_type: Flow
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:77b3f2a6-a8a3-4481-944a-58fb9f23fdda
tags:
- send-money
- 转账
- KYC
- 退款
subdomain: null
module: null
sensitivity: normal
name: Send Money 端到端转账流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Send Money 端到端转账流程覆盖发送转账、收款人领取（已KYC / 未KYC 两种路径）、以及订单过期退款的全过程。与手机号转账不同，Send Money 不经过付款人中间户，资金流为「付款人 → 收款人」直连结算。

## 步骤(跨系统)

### 5.1 发送转账
付款人发起 Send Money 转账请求，系统创建转账订单。

### 5.2 发送和领取（收款人已KYC）
- 资金流：付款人 → 收款人（自动结算）
- 领取方式：付款时直接自动结算给收款人，无需收款人手动操作
- 通知：
  - 付款方：转账成功聊天气泡通知
  - 收款方：转账到账聊天气泡通知
- 异常：自动领取失败时，24H 退款给付款人；该路径下只会出现支付失败

### 5.3 收款人完成KYC（收款人未KYC 场景）
- 资金流：付款人（手动结算）→ 收款人
- 发送阶段：聊天气泡通知收款人有转账
- 领取阶段：收款人完成 KYC 后，系统自动结算领取（仍存在结算失败的可能）

### 5.4 订单过期
- 收款人未KYC 且未在规定时限内完成领取：72H 退款，发送聊天气泡通知给付款方
- 收款人已KYC 自动领取失败：24H 退款

## 涉及服务/表
原文未明确列出具体服务与表名（数据库设计图以图片形式给出，未能提取）。

## 校验点
- 收款人 KYC 状态判定：决定走自动结算（已KYC）还是手动结算待领取（未KYC）路径
- 自动结算结果校验：已KYC 路径下自动领取失败需触发 24H 退款
- 订单时效校验：未KYC 收款人未在 72H 内完成 KYC 领取，触发过期退款
- 通知通道一致性：Send Money 全流程使用聊天气泡通知（区别于手机号转账的公众号通知 + 短信）
