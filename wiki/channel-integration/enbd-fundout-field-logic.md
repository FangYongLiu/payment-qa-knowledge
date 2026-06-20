---
title: ENBD出款字段逻辑
domain: channel-integration
kind: wiki_page
slug: enbd-fundout-field-logic
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD出款字段逻辑

本页梳理 ENBD 渠道出款时的两类关键字段：`countryCode`/`cityCode` 的获取来源，以及 `Remark` 字段在不同场景下的取值与覆盖规则。完整出款流程见 [[flow_enbd_fundout]]。

## countryCode / cityCode 获取逻辑

- ENBD 与 INNER 子渠道无需传 `cityCode` 信息。
- 仅在收款为**他行 IBAN**时，渠道才会调用 member 查询 city name。
- 即：本行 IBAN（INNER）跳过 city name 查询，跨行场景才补齐 city 字段。

## Remark 字段处理逻辑

Remark 的取值按以下优先级/规则处理：

1. **默认值**：使用 `memo` 字段（提现场景：Fundout）。
2. **memo 为空时**：使用 `FIS` 或 `MWO`（目前暂无为空场景）
   - `purposeCode = FIS`：提现
   - `purposeCode = MWO`：转账到卡
3. **useMerchantName 配置中的商户**：memo 拼接为 `商户名称 + 地址`。
4. **merchantDynamic 配置中的商户**：直接替换 memo 内容。

## 相关链接

- 渠道与子渠道编码（ENBD201/204/205 等）：见 [[enbd-channel-overview]]
- 出款整体流程与渠道余额校验：[[flow_enbd_fundout]]
- 余额校验依赖的查询任务：[[auto_enbd_balance_monitor_job]]
- 余额不足报错处理：[[ts_enbd_channel_balance_not_enough]]
