---
id: scn_chargeback_mail_send_cases
object_type: Scenario
domain: risk-control
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1333395487
tags:
- chargeback
- mail
- test-cases
subdomain: chargeback
module: mail-notification
sensitivity: normal
name: ChargeBack邮件发送测试场景集
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
ChargeBack页面上传收单行文件（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY），新增ChargeBack记录后触发邮件发送逻辑。

## 前置条件
- 邮件相关配置已在 `Basis → RISK CONTROL → Data Analysis → Risk System Param` 设置：
  - `chargeback_mail_send_outer_switch`（邮件总开关）
  - `chargeback_mail_send_to_default`（默认邮件地址）
  - `chargeback_mail_send_external_default`（外部邮件地址）
  - `chargeback_mail_send_psp_default`（PSP默认6邮箱）
  - `chargeback_mail_receiver_partner_XXXX`（partner_name邮箱配置）
- 商户类型判定依据：`Label=Total Process` → PSP商户；否则非PSP商户。
- 商户邮箱来源：商户的 Administrator Contact Email；ReferredId 邮箱来自 refers 商户的 Administrator Contact Email。

## 操作步骤
按下表组合触发条件，构造对应记录并上传文件触发邮件发送：

| 编号 | 邮件开关`chargeback_mail_send_to_default` | Merchant_Type | 有ReferredId | ReferedId_Email | External | partner_name | Merchant_Email |
|---|---|---|---|---|---|---|---|
| TS001 | Yes | - | - | - | - | - | - |
| TS002 | No | PSP | 有 | 有 | - | - | - |
| TS003 | No | PSP | 有 | 无 | - | - | 有 |
| TS004 | No | PSP | 有 | 无 | - | - | 无 |
| TS005 | No | PSP | 无 | - | - | - | 有 |
| TS006 | No | PSP | 无 | - | - | - | 无 |
| TS007 | No | 非PSP | - | - | 是 | 有 | - |
| TS008 | No | 非PSP | - | - | 是 | 否 | 有 |
| TS009 | No | 非PSP | 是 | 否 | - | - | 无 |
| TS010 | No | 非PSP | - | - | 否 | 有 | - |
| TS011 | No | 非PSP | - | - | 否 | 否 | 有 |
| TS012 | No | 非PSP | - | - | 否 | 否 | 无 |

判断顺序：
1. 邮件开关 Yes → 发默认配置邮件；No → 走商户邮件逻辑。
2. PSP判定：`Label=Total Process` 为PSP，否则非PSP。
3. PSP分支：先查 ReferredId → 有则查referredId对应商户邮箱；无则查PSP商户自身邮箱；最终叠加 PSP默认6邮箱 + 默认邮箱。
4. 非PSP分支：先判 External，再判 partner_name，再判商户邮箱；按命中情况叠加 partner_name邮箱 / 外部地址 / 商户邮箱 / 默认邮箱。

## DB 校验点
- 记录写入需为 New case（`aml.t_chargeback_pool` 状态 NC）才会触发邮件发送。
- 历史记录（Excel `history flag` 有值）不发邮件、不冻结，仅同步 CasePool。
- 邮件配置读取自 Risk System Param（更改后需刷缓存）。

## 预期结果
| 编号 | 预期收件人 |
|---|---|
| TS001 | 默认配置的邮箱 |
| TS002 | referredId对应邮箱 + PSP默认6邮箱 + 默认邮箱 |
| TS003 | 商户邮箱 + PSP默认6邮箱 + 默认邮箱 |
| TS004 | PSP默认6邮箱 + 默认邮箱 |
| TS005 | 商户邮箱 + PSP默认6邮箱 + 默认邮箱 |
| TS006 | PSP默认6邮箱 + 默认邮箱 |
| TS007 | partner_name配置邮箱 + 外部地址 + 默认邮箱 |
| TS008 | 商户邮箱地址 + 外部地址 + 默认邮箱 |
| TS009 | 外部地址 + 默认邮箱 |
| TS010 | partner_name配置邮箱 + 默认邮箱 |
| TS011 | 商户邮箱 + 默认邮箱 |
| TS012 | 默认邮箱 |

详见 [[chargeback-mail-notification]] 与 [[chargeback-mail-config]]。
