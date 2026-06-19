---
title: ChargeBack冻结逻辑
domain: risk-control
kind: wiki_page
slug: chargeback-freeze-logic
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: []
---

# ChargeBack冻结逻辑

ChargeBack 文件解析后，针对 New case 记录会自动对收款方商户的 DPM 账户进行资金冻结，并将冻结记录写入 `aml.t_freeze_order`。

## 触发条件

- 仅当新增的 ChargeBack 记录为 **New case (NC)** 时触发冻结。
- 冻结操作在记录同步到 `aml.t_risk_case` 之后执行。
- 非 New case 的历史记录（依据 Excel 中的 `history flag` 判定）**不触发冻结**。
- 相关上下游处理见 [[chargeback-casepool-sync]] 与 [[chargeback-mail-notification]]。

## 冻结对象与记录格式

冻结对象统一为 **merchantId（收款方）** 的 DPM 账户中的**交易金额**，但记录写入 `aml.t_freeze_order` 时，PSP 与非 PSP 商户的 Memo / Extension 格式不同：

| 商户类型 | 冻结对象 | Memo | Extension |
|---|---|---|---|
| PSP 商户 | merchantId（收款方）DPM 账户交易金额 | `CHB + ARN + auto freeze` | `caseId`（=`aml.t_chargeback_pool.id`）+ `ARN` |
| 非 PSP 商户 | merchantId（收款方）DPM 账户交易金额 | `CHB + paymentOrderNo + auto freeze` | `caseId` + `paymentOrderNo` |

PSP 商户判定标准：商户 `Label = Total Process`。

## 冻结白名单配置

- 配置路径：`Basis → RISK CONTROL → Data Analysis → Risk System Param`
- 参数名：`chargeback_ignore_frozen_merchant_list`
- 作用：名单内的商户 ID 将被忽略，不执行冻结。
- 修改后需**刷缓存**生效。
- 其他相关参数见 [[chargeback-config-params]]。

## 关联说明

- Case 状态枚举与 NC 判定参考 [[chargeback-case-status]]。
- 业务全景与端到端处理参考 [[chargeback-business-overview]] 与 [[flow_chargeback_processing]]。
