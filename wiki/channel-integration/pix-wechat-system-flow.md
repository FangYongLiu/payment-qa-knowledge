---
title: PIX微信MPC系统流程设计
domain: channel-integration
kind: wiki_page
slug: pix-wechat-system-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: []
---

# PIX微信MPC系统流程设计

本页梳理 PIX 微信 MPC（Merchant Presented Code）渠道在扫码解析、创建交易、查询、退款、关单、最终支付结果与对账等环节的系统流程、关键动作与责任分工。汇率同步规则见 [[pix-wechat-rate-sync]]，渠道总览见 [[pix-wechat-mpc-overview]]，端到端流程图见 [[flow_pix_wechat_mpc_payment]]。

## 扫码解析（Scan and parse code）

参考：pix-SD-MPC

| Step | System | Function |
|---|---|---|
| 1.3.1.1 `MpcFacade.parseCode` | pix-wechat | 调用 vendor 获取 merchant information；将 merchant code 信息（含 rate 信息）保存到 ES |

- Vendor API: Requester `QUERY_MERCHANT_CODE`
- 注意点：外汇维护方为 Remittance Team
- Owner：Business Developer

## 创建交易并支付（Create trade and pay）

参考：pix-SD-MPC、pix-SD-Transaction

| Step | System | Function |
|---|---|---|
| confirm trade information | wallet | 按 rate 计算应支付的 AED 金额（App Team） |
| 1 `MpcFacade.creatTrade` | pix-wechat | 从 ES 取 merchant code 信息；在 vendor 创建 trade order；创建收银台 trade order 并返回 `cashierUrl`；按 rate config 校验金额（Owner: Zhibin Liu） |
| 2.1 process result | pix-wechat | 处理 trade order 通知；调用 vendor 通知支付结果；调用 query 保存账单；调用 reconciliation 保存 fundout glide |
| - | tradeii / pfs / payment | 从 cmf 取 inst order no 保存进 tradeii，并提供变更 api（Owner: Yu Tang, Dewen Li） |
| other | pix-wechat | bill synchronization（Owner: Zhibin Liu） |
| other | bill | bill configuration UI（Owner: Yongxin Cao） |
| other | reconciliation | reconciliation configuration（Owner: Yibin Xia） |

- Vendor API：Requester `SCAN_CODE_FOR_PAYMENT`、Requester `NOTIFY_PAYMENT_RESULT`
- 关键点：从 tradeii 获取 `instOrderNo`（关键字 `DbtrBankId`）

## 查询交易结果（Query trade result）

参考：pix-SD-MPC

| Step | System | Function | Owner |
|---|---|---|---|
| `MpcFacade.parseCode` | pix-wechat | 实现 dubbo facade | Zhibin Liu |

- Vendor API：Responder `QUERY_PAYMENT_ORDER_INFO`

## 退款（Refund）

参考：pix-SD-Transaction，详细流程见 [[flow_pix_wechat_refund]]。

| Step | System | Function |
|---|---|---|
| 1.1 refund | pix | 实现 vendor api；执行必要的退款检查并异步请求退款，返回 vendor success；通知退款账单 |
| other | pix | bill synchronization |
| other | bill | bill configuration UI（Owner: Yongxin Cao） |
| other | reconciliation | reconciliation configuration（Owner: Yibin Xia） |

- 退款金额规则：`Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount`
- Vendor API：Responder `REFUND`
- 退款无异步响应，由微信在 10 分钟内通过 `QUERY_REFUND_ORDER_INFO` 查询；超时后通过 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` 推定退款成功

## 关单（Close Payment）

| Step | System | Function |
|---|---|---|
| 1 close payment | pix | 实现 vendor api；关闭交易；注意微信关单逻辑 |

- Vendor API：Responder `CLOSE_PAYMENT`

## 最终支付结果（Final payment result）

| Step | System | Function |
|---|---|---|
| 1 process final payment result | pix | 实现 vendor api；若最终支付失败则退款 trade |

- Vendor API：Responder `NOTIFY_FINAL_PAYMENT_RESULT`

## 其他接口（Other）

| Item | System | Function | 说明 |
|---|---|---|---|
| query payment | pix | 实现 vendor api | 查询本地 trade 状态 |
| query refund | pix | 实现 vendor api | `QUERY_REFUND_ORDER_INFO` |
| notify final refund | pix | 实现 vendor api | `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` |

退款推定说明：实际是在多次查询及长时间（10 分钟）无结果后才会执行推定；默认只推定通知 1 次，一旦推定即按退款成功处理。钱包可通过次日账单获得推定的交易记录。

字段及Q&A详见 [[pix-wechat-qa-notes]]，全量 Vendor API 清单见 [[pix-wechat-vendor-api-catalog]]。

## 对账（Reconciliation）

需通过特定 api 下载对账文件，详细流程见 [[flow_pix_wechat_reconciliation]]。

| Step | System | Function |
|---|---|---|
| 1 download check file | pix | 用 vendor api 下载文件并通过 ufs 保存；将 `fileTag` 存入 db |
| 2 auto reconciliate | reconciliation | 配置自动对账 job；定义 dubbo api（Owner: Yibin Xia） |
| 2.1 get file | pix | 返回 `fileTag` |

- Vendor API：Requester `QUERY_BILL_ADDRESS`
