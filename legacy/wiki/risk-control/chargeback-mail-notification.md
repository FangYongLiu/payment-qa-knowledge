---
title: ChargeBack邮件发送逻辑
domain: risk-control
kind: wiki_page
slug: chargeback-mail-notification
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: []
---

# ChargeBack邮件发送逻辑

ChargeBack 记录新增后，系统按照「邮件总开关 → 商户类型 → ReferredId → 外部商户/partner_name → 商户邮箱」的多级判断决定收件人。本页梳理判断顺序和 12 种典型测试场景。相关参数配置见 [[chargeback-config-params]]，整体业务上下文见 [[chargeback-business-overview]]。

## 判断顺序

1. **邮件开关** `chargeback_mail_send_to_default`
   - `Yes`：仅发送默认配置邮箱
   - `No`：进入商户维度判断
2. **判断是否 PSP 商户**
   - `Label = Total Process` → PSP 商户
   - `Label != Total Process` → 非 PSP 商户
3. **PSP 商户分支：判断是否有 ReferredId**
   - 有 ReferredId：
     - 该 ReferredId 商户配置了 Administrator Contact Email → 发送 `referredId 对应邮箱 + PSP 默认 6 邮箱 + 默认邮箱`
     - 未配置 → 回落到 PSP 商户自身邮箱判断
   - 无 ReferredId：
     - PSP 商户配置了邮箱 → 发送 `商户邮箱 + PSP 默认 6 邮箱 + 默认邮箱`
     - 未配置 → 发送 `PSP 默认 6 邮箱 + 默认邮箱`
4. **非 PSP 商户分支：判断是否外部商户 (External)**
   - 外部商户：
     - 有 `partner_name` → `partner_name 配置邮箱 + 外部地址 + 默认邮箱`
     - 无 `partner_name`，商户配置邮箱 → `商户邮箱 + 外部地址 + 默认邮箱`
     - 无 `partner_name` 且无商户邮箱 → `外部地址 + 默认邮箱`
   - 非外部商户：
     - 有 `partner_name` → `partner_name 配置邮箱 + 默认邮箱`
     - 无 `partner_name`，商户配置邮箱 → `商户邮箱 + 默认邮箱`
     - 都无 → 仅发送默认邮箱

> 注：`partner_name` 分支正常业务无匹配场景，目前主要用于 remittance 渠道。

## 关键概念

- **ReferredId_Email**：referrer 商户的 Administrator Contact Email
- **Merchant_Email**：当前商户的 Administrator Contact Email（Email 在商户资料中为必填字段）
- **PSP 默认 6 邮箱**：`chargeback_mail_send_psp_default` 配置项
- **外部地址**：`chargeback_mail_send_external_default` 配置项
- **partner_name 邮箱**：`chargeback_mail_receiver_partner_XXXX` 配置项
- **默认邮箱**：`chargeback_mail_send_to_default` 配置项

## 12 种测试场景

完整的 TS001~TS012 用例矩阵（覆盖开关开/关、PSP/非 PSP、是否有 ReferredId、是否外部商户、是否有 partner_name、是否有商户邮箱的组合）见 [[scn_chargeback_mail_send_cases]]。

要点速查：

- **TS001**：邮件开关 = Yes → 仅默认邮箱
- **TS002~TS006**：PSP 商户分支，结果基于 ReferredId 与商户邮箱组合
- **TS007~TS009**：非 PSP + 外部商户分支
- **TS010~TS012**：非 PSP + 非外部商户分支

## 触发前提

- 邮件发送仅对 **New case (NC)** 记录生效；非 New case（历史记录，依据 Excel 的 `history flag` 字段判断）只同步 CasePool，**不发邮件**、**不冻结**。详见 [[chargeback-case-status]]。
- 同次处理中还会触发 [[chargeback-freeze-logic]] 与 [[chargeback-casepool-sync]]。
- 端到端流程参见 [[flow_chargeback_processing]]。
