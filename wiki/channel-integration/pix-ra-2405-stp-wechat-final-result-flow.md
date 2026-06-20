---
title: pix-RA-2405-STP-Wechat 最终支付结果处理流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-final-result-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:dba7bdbd-2d6f-4da2-9e77-7bd4f162dc7b
tags: []
---

# pix-RA-2405-STP-Wechat 最终支付结果处理流程

描述 Tenpay 通知 pix 最终支付结果后，pix 针对"支付失败但钱包成功"场景执行退款补偿，确保两侧状态一致。

## 参与方

- **vendor(Tenpay)**：外部支付渠道，负责回传最终支付结果。
- **pix**：渠道集成侧，接收最终结果并决策后续补偿动作。
- **tradeii**：交易/钱包侧，承接退款指令。

## 流程步骤

1. **vendor(Tenpay) → pix**：`process final payment result`，通知最终支付结果。
2. **条件分支 alt `[final payment failed but wallet successful]`**：
   - **pix → tradeii**：`refund`，发起退款以冲销钱包侧的成功状态。

## 关键说明

- 仅当**最终支付失败**且**钱包步骤成功**时，pix 才触发对 tradeii 的 `refund` 调用。
- 该分支为故障恢复路径，用于保持渠道与钱包两侧最终状态一致；图中未展开其他分支。
