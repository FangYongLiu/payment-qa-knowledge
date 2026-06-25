---
id: scn_remittance_send_money
object_type: Scenario
name: Send Money 转账(KYC 分支 / 退款 / 通知)
aliases: [Send Money 测试场景]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/185794690; wiki:77b3f2a6-a8a3-4481-944a-58fb9f23fdda
tags: [send-money, transfer, kyc, refund]
related_services: [svc_cashierii, svc_tradeii, svc_transfer, svc_pns]
related_tables: []
related_logs: []
---

# Send Money 转账(KYC 分支 / 退款 / 通知)

## 触发 / 入口
- 入口:Botim 消息窗进入 Send Money,付款人选择收款人并发起转账。
- 需求来源:Wallet Redesign - Send Money(Send 需求文档 + Figma Local Transfer)。

## 关联关系
- **涉及服务**:[[svc_cashierii]]、[[svc_tradeii]]、[[svc_transfer]]、[[svc_pns]](= `related_services`;未注册收款人走短信服务 mns,对象待补)
- **校验的表**:待补(Send Money 订单 / 领取状态 / 退款记录,原文 ER 图未解析)
- **端到端流程**:[[flow_remittance_send_money]]
- **相关日志**:待补

## 前置条件
- 付款人已注册且可支付;收款人可处于「已注册已 KYC」「已注册未 KYC」「未注册」三种状态之一。

## 操作步骤(按子场景)
### 1. 发送转账
1. 付款人选择收款人并发起 Send Money 转账。
2. 按收款人 KYC 状态决定资金流走向:
   - 已 KYC:付款人 →(自动结算)→ 收款人。
   - 未 KYC:付款人 →(手动结算 / 待领取)→ 收款人。
3. 付款方收到转账成功的聊天气泡通知。

### 2. 发送和领取
- 已 KYC:付款时直接自动结算给收款人,收款方收到到账聊天气泡通知。
- 未 KYC:聊天气泡通知收款人有转账待领取,款项处于待领取状态;自动领取存在失败可能(已 KYC 失败时走 24H 退款)。

### 3. 收款人完成 KYC
- 未 KYC 收款人在转账存续期内完成 KYC 后,系统自动结算领取(仍可能失败)。
- 自动结算成功后按 Send Money 规则发送聊天气泡通知双方。

### 4. 订单过期
- 未 KYC:72H 内未完成 KYC / 领取,订单过期触发退款,聊天气泡通知付款方。
- 已 KYC:仅自动领取失败时走 24H 退款,不存在长时间未领取过期(仅可能支付失败)。

## DB 校验点
- 待补:Send Money 订单状态(待领取 / 已领取 / 已退款)、领取状态、退款记录(原文数据库设计图未解析)。

## 预期结果
- 已 KYC:自动结算到账,双方收到聊天气泡通知。
- 未 KYC 且按时完成 KYC:系统自动结算领取并通知。
- 未 KYC 超时:72H 后退款,付款方收到聊天气泡通知。

## 与手机号转账的对比(QA 关注差异)
| 维度 | 手机号转账 | Send Money |
| --- | --- | --- |
| 资金流(已/未 KYC) | 付款人 → 付款人中间户 → 收款人 | 付款人 →(自动/手动结算)→ 收款人(点对点) |
| 未 KYC 领取 | 公众号通知,KYC 后用户手动领取 | 聊天气泡通知,KYC 后系统自动结算领取 |
| 未 KYC 退款 | 24H,公众号通知 | 72H,聊天气泡通知 |
| 已 KYC 退款 | 自动领取失败 24H 退款 | 仅出现支付失败 |
| 通知载体 | 公众号 / 短信(收款方收款成功短信 + 公众号) | 全程聊天气泡(付款方转账成功 / 收款方到账) |

> 不确定 / 缺失的点已标「待补」,留待人工补充。
