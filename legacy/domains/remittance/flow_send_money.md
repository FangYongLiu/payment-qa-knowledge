---
id: flow_send_money
object_type: Flow
domain: remittance
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/185794690
tags:
- send-money
- transfer
- kyc
- refund
subdomain: null
module: null
sensitivity: normal
name: Send Money端到端转账流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Send Money 端到端转账流程，覆盖从付款人发起转账，到收款人领取(分已KYC/未KYC两种路径)，以及订单过期触发退款的完整业务链路。与手机号转账不同，Send Money 在收款人已KYC时走自动结算，未KYC时通过聊天气泡通知，KYC完成后由系统自动结算领取。

## 步骤(跨系统)
1. **发送转账**：付款人发起 Send Money 转账订单。
2. **发送和领取**(收款人已KYC)：付款人 → 收款人，自动结算；付款方收到转账成功聊天气泡通知，收款方收到转账到账聊天气泡通知。
3. **收款人完成KYC**(收款人未KYC)：付款人 → 收款人，手动结算路径；收款人通过聊天气泡通知得知有转账，完成 KYC 后由系统自动结算领取(仍可能存在结算失败)。
4. **订单过期/退款**：
   - 收款人未KYC：72H 未领取触发退款，发送聊天气泡通知。
   - 收款人已KYC：自动领取失败时 24H 退款；正常路径下只会出现支付失败。

## 涉及服务/表
原文未给出具体服务与表名(数据库设计图未能下载解析)。

## 校验点
- 收款人 KYC 状态判定：决定走自动结算还是手动结算/待领取路径。
- 自动结算成功/失败判定：失败需进入 24H 退款流程。
- 订单过期时限：未KYC 场景 72H，未自动领取场景 24H。
- 通知通道一致性：付款方与收款方均通过聊天气泡通知(区别于手机号转账的公众号/短信通知)。

</target>
