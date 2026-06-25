---
id: scn_online_business_merchant_async_notify
object_type: Scenario
name: 商户异步通知接收与重试 (Open API)
aliases: [异步通知, async-notifications, merchant-notify, 支付结果通知]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p17 (payby-merchant-api-async-notifications)
tags: [online-business, open-api, 异步通知, 商户接入, 幂等, 重试]
related_services: [svc_pns, svc_sgs]
related_tables: []
related_logs: []
---

# 商户异步通知接收与重试 (Open API)

> Open API 商户接入测试场景:PayBy 在订单状态变化/资金事件发生时,以数据流向商户后台推送异步通知,商户须按统一规范接收处理并应答。来源:PayBy 开放接口文档 v2.25。

## 触发 / 入口
订单状态变化或资金事件发生时,PayBy 通过 [[svc_pns]](通知服务)向商户配置的 `notifyUrl` 推送异步通知。涵盖以下通知类型:

| 通知类型 | 参数变量名 | 参数类型 |
| --- | --- | --- |
| 支付结果通知 | `acquireOrder` | AcquireOrder |
| 退款结果通知 | `refundOrder` | RefundOrder |
| 付款到账户成功通知 | `payToBalanceOrder` | RefundOrder |
| 付款到银行卡成功通知 | `payToCardOrder` | PayToCardOrder |
| 拒付通知 (Chargeback) | `acquireChargeback` | AcquireChargeback |
| VAM 充值通知 | `vamDepositOrder` | VamDepositOrder(见 [[api_payby_notify_vam_deposit]]) |

## 关联关系
- **涉及服务**:[[svc_pns]](通知服务,对外推送)、[[svc_sgs]](开放网关)(= `related_services`)。
- **读写的表**:待补(商户 webhook 配置/通知流水表,具体表待补)。
- **相关日志**:`service:pns`(= `related_logs`)。

## 前置条件
- 商户已配置可接收通知的 `notifyUrl`。
- 商户系统具备幂等处理能力(同一通知可能多次到达)。

## 操作步骤(QA 验证点)
1. **统一应答格式**:商户收到任意通知后必须返回 `{"response":"SUCCESS"}`,表示成功接收;返回其他任意内容均视为异常并触发重试。
2. **幂等(重复通知)**:同一通知可能多次发送,商户系统必须能正确处理重复通知。验证重复推送同一 `notify_id` 时商户业务不重复执行。
3. **失败重试策略**:应答不符合规范或超时即判定失败并重发,直到成功为止(但不保证最终一定成功)。
   - 默认重试 **7 次**,时间间隔(分钟):**2, 10, 10, 60, 120, 360, 900**。
4. **兜底**:订单状态不明或未收到通知时,商户应主动调用查订单接口确认;对账用 [[api_payby_get_order_statement]] 下载对账单核对。

## DB 校验点
- 通知推送流水、重试次数与最终状态:待补(原文未提供库表)。

## 预期结果
- 商户正确应答 `{"response":"SUCCESS"}` 后停止重试;未正确应答触发上述 7 次退避重试。
- 幂等场景下重复通知不导致商户侧重复入账/重复发货。

## 通知样例(VAM 充值)
```
Http Body
{
  "notify_time": "20241224061738",
  "vamDepositOrder": {
    "remitterInfo": "MR HUA JIANG",
    "amount": { "amount": 3000, "currency": "AED" },
    "orderNo": "131727701521486397",
    "referenceNo": "UFOC0HQ008",
    "senderBankCode": "BBMEAEADXXX",
    "status": "SUCCESS"
  },
  "_input_charset": "UTF-8",
  "notify_timestamp": 1735006658869,
  "notify_id": "202409300013926551"
}
```
