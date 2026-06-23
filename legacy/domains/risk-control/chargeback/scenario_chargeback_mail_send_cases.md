---
id: scn_chargeback_mail_send_cases
object_type: Scenario
domain: risk-control
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
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
ChargeBack页面上传收单行文件（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY），新增ChargeBack记录后，触发邮件发送逻辑。详细规则参见 [[chargeback-mail-notification]]。

## 前置条件
- 配置路径：Basis → RISK CONTROL → Data Analysis → Risk System Param
- 邮件总开关 `chargeback_mail_send_outer_switch` = yes
- 业务产品码在 `chargeback_send_mail_product_config` 白名单内
- 相关配置项准备：
  - `chargeback_mail_send_to_default`（默认邮箱）
  - `chargeback_mail_send_external_default`（外部邮件地址）
  - `chargeback_mail_send_psp_default`（PSP默认6个邮箱）
  - `chargeback_mail_receiver_partner_XXXX`（partner_name配置）
- 商户类型判定依据：Label=Total Process → PSP；Label!=Total Process → 非PSP
- 仅 New case 记录会发送邮件，历史记录（history flag 有值）不发送

## 操作步骤
按以下12个测试场景分别构造数据并上传ChargeBack文件，校验发送邮箱地址。

| TS | chargeback_mail_send_to_default | Merchant_Type | ReferredId | ReferedId_Email | External | partner_name | Merchant_Email |
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

注：Email为必填字段，"无"指对应商户的Administrator Contact Email缺失场景。

## DB 校验点
- `aml.t_chargeback_pool`：新增记录、case 状态为 New case (NC)
- 商户Label判定（Total Process 与否）影响 PSP/非PSP 分支
- referredId 对应商户的 Administrator Contact Email
- 商户 Administrator Contact Email
- Risk System Param 中各邮件配置项取值

## 预期结果
| TS | 预期发送邮箱地址 |
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

判断顺序：① 邮件开关 → ② PSP/非PSP（Label=Total Process）→ ③ PSP分支：referredId → 商户邮箱 → PSP默认6邮箱+默认邮箱；④ 非PSP分支：External → partner_name → 商户邮箱 → 外部地址/默认邮箱。
