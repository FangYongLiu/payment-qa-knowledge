---
title: ChargeBack邮件发送逻辑
domain: risk-control
kind: wiki_page
slug: chargeback-mail-notification
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack邮件发送逻辑

ChargeBack 记录新增后会触发邮件通知，发送对象由邮件总开关、商户类型、ReferredId、外部商户标识、partner_name 与商户邮箱等多重条件共同决定。

## 判断顺序

按以下顺序逐层判断收件人：

1. **邮件开关** `chargeback_mail_send_to_default`
   - `Yes`：仅发送至默认配置的邮箱
   - `No`：进入下一层，按商户邮箱链路发送
2. **是否 PSP 商户**
   - `Label = Total Process` → PSP 商户
   - `Label != Total Process` → 非 PSP 商户
3. **PSP 商户分支**：先看是否有 ReferredId
   - 有 ReferredId：查找 ReferredId 对应的 Administrator Contact Email
     - 有 → ReferredId 邮箱 + PSP 默认 6 邮箱 + 默认邮箱
     - 无 → 再查 PSP 商户自身邮箱
       - 有 → 商户邮箱 + PSP 默认 6 邮箱 + 默认邮箱
       - 无 → PSP 默认 6 邮箱 + 默认邮箱
   - 无 ReferredId：查 PSP 商户自身邮箱
     - 有 → 商户邮箱 + PSP 默认 6 邮箱 + 默认邮箱
     - 无 → PSP 默认 6 邮箱 + 默认邮箱
4. **非 PSP 商户分支**：判断 External 标识
   - **外部商户**：再判断 partner_name
     - 有 partner_name → partner_name 配置邮箱 + 外部地址 + 默认邮箱
     - 无 partner_name → 看商户邮箱
       - 有 → 商户邮箱 + 外部地址 + 默认邮箱
       - 无 → 外部地址 + 默认邮箱
   - **非外部商户**：再判断 partner_name
     - 有 partner_name → partner_name 配置邮箱 + 外部地址 + 默认邮箱
     - 无 partner_name → 看商户邮箱
       - 有 → 商户邮箱 + 默认邮箱
       - 无 → 默认邮箱

## 测试场景矩阵（TS001–TS012）

判断维度：邮件开关 `chargeback_mail_send_to_default`、Merchant_Type、是否有 ReferredId、ReferredId_Email（refers 商户的 Administrator Contact Email）、External、partner_name（正常无，用于 remittance）、Merchant_Email（商户的 Administrator Contact Email）。

| 编号 | 开关 | 商户类型 | ReferredId | ReferredId_Email | External | partner_name | Merchant_Email | 预期发送邮箱 |
|---|---|---|---|---|---|---|---|---|
| TS001 | Yes | - | - | - | - | - | - | 默认配置的邮箱 |
| TS002 | No | PSP | 有 | 有 | - | - | - | ReferredId 邮箱 + PSP 默认 6 邮箱 + 默认邮箱 |
| TS003 | No | PSP | 有 | 无 | - | - | 有 | 商户邮箱 + PSP 默认 6 邮箱 + 默认邮箱 |
| TS004 | No | PSP | 有 | 无 | - | - | 无 | PSP 默认 6 邮箱 + 默认邮箱 |
| TS005 | No | PSP | 无 | - | - | - | 有 | 商户邮箱 + PSP 默认 6 邮箱 + 默认邮箱 |
| TS006 | No | PSP | 无 | - | - | - | 无 | PSP 默认 6 邮箱 + 默认邮箱 |
| TS007 | No | 非 PSP | - | - | 是 | 有（正常无） | - | partner_name 配置邮箱 + 外部地址 + 默认邮箱 |
| TS008 | No | 非 PSP | - | - | 是 | 否 | 有 | 商户邮箱 + 外部地址 + 默认邮箱 |
| TS009 | No | 非 PSP | 是 | 否 | - | - | 无 | 外部地址 + 默认邮箱 |
| TS010 | No | 非 PSP | - | - | 否 | 有（正常无） | - | partner_name 配置邮箱 + 默认邮箱 |
| TS011 | No | 非 PSP | - | - | 否 | 否 | 有 | 商户邮箱 + 默认邮箱 |
| TS012 | No | 非 PSP | - | - | 否 | 否 | 无 | 默认邮箱 |

> Email 在商户配置中是必填字段，"无 Merchant_Email / ReferredId_Email" 属于异常或缺失场景。

## 触发前置条件

- 仅 **New case** 记录会发送邮件；非 New case 的历史记录（Excel `history flag` 有值）只同步 CasePool，不发邮件、不触发冻结。详见 [[chargeback-case-status]]。
- 邮件相关开关与地址列表见 [[chargeback-mail-config]]。
- 端到端流转参考 [[chargeback-process-flow]] 与 [[flow_chargeback_processing]]；测试用例集见 [[scn_chargeback_mail_send_cases]]。
