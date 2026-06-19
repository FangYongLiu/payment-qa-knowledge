---
title: ChargeBack冻结逻辑
domain: risk-control
kind: wiki_page
slug: chargeback-freeze-logic
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack冻结逻辑

ChargeBack冻结逻辑用于在新增 New case 时，对收款方商户的DPM账户中对应交易金额执行自动冻结，并支持通过白名单豁免特定商户。

## 触发条件

- 仅当新增的ChargeBack记录为 **New case (NC)** 时触发冻结。
- 冻结动作在记录同步到 `aml.t_risk_case` 之后执行。
- 非 New case 记录（历史记录）**不触发冻结**。
- 相关上下文见 [[chargeback-case-status]] 与 [[chargeback-process-flow]]。

## 冻结对象与记录信息

冻结对象统一为 **merchantId（收款方）** 在DPM账户中的 **交易金额**，记录写入 `aml.t_freeze_order`。Memo 与 Extension 内容按商户类型区分：

| 商户类型 | 冻结对象 | Memo | Extension |
|---|---|---|---|
| **PSP商户** | merchantId（收款方）DPM账户的交易金额 | `CHB + ARN + auto freeze` | `caseId`（`aml.t_chargeback_pool.id`） + `ARN` |
| **非PSP商户** | merchantId（收款方）DPM账户的交易金额 | `CHB + paymentOrderNo + auto freeze` | `caseId` + `paymentOrderNo` |

## 冻结白名单配置

支持通过白名单忽略指定商户的自动冻结。

- 配置路径：`Basis → RISK CONTROL → Data Analysis → Risk System Param`
- 配置项：`chargeback_ignore_frozen_merchant_list`
- 内容：商户ID列表，命中即跳过冻结。
- 注意：**配置更改后需刷缓存**才能生效。

## 相关链接

- 触发前置同步：[[chargeback-casepool-sync]]
- 同流程的邮件分支：[[chargeback-mail-notification]]
- 业务全貌：[[chargeback-business-overview]]
