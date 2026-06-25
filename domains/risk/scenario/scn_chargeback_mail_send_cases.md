---
id: scn_chargeback_mail_send_cases
object_type: Scenario
name: ChargeBack邮件发送测试场景集
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags:
- chargeback
- mail
- test-cases
related_tables:
- tbl_aml_t_system_param
---

# ChargeBack邮件发送测试场景集

## 触发/入口
ChargeBack 页面上传收单行文件(VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY),新增 ChargeBack 记录后触发邮件发送逻辑。整体流程见 [[flow_chargeback_processing]]。

## 关联关系
- **校验的表**:[[tbl_aml_t_system_param]](邮件配置项所在表,= `related_tables`);`aml.t_chargeback_pool`(待补:未建对象)。
- **所属流程**:[[flow_chargeback_processing]]

## 前置条件
- 配置路径:Basis → RISK CONTROL → Data Analysis → Risk System Param([[tbl_aml_t_system_param]])。
- 邮件总开关 `chargeback_mail_send_outer_switch` = yes;业务产品码在 `chargeback_send_mail_product_config` 白名单内。
- 相关配置项:`chargeback_mail_send_to_default`(默认邮箱)、`chargeback_mail_send_external_default`(外部地址)、`chargeback_mail_send_psp_default`(PSP 默认 6 邮箱)、`chargeback_mail_receiver_partner_XXXX`(partner_name 配置)。
- 商户类型判定:Label=Total Process → PSP;Label!=Total Process → 非 PSP。
- 仅 New case 记录发邮件,历史记录(history flag 有值)不发送。

## 操作步骤
按下列 12 个测试场景分别构造数据并上传 ChargeBack 文件,校验发送邮箱地址。

| TS | mail_send_to_default | Merchant_Type | ReferredId | ReferedId_Email | External | partner_name | Merchant_Email |
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

注:"无"指对应商户的 Administrator Contact Email 缺失。

## DB 校验点
- `aml.t_chargeback_pool`:新增记录、case 状态为 New case (NC)(待补:未建对象)。
- 商户 Label 判定(Total Process 与否)影响 PSP/非 PSP 分支。
- referredId 对应商户的 Administrator Contact Email、商户自身 Administrator Contact Email。
- Risk System Param 中各邮件配置项取值。

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

判断顺序:① 邮件开关 → ② PSP/非PSP(Label=Total Process)→ ③ PSP 分支:referredId → 商户邮箱 → PSP默认6邮箱+默认邮箱;④ 非PSP 分支:External → partner_name → 商户邮箱 → 外部地址/默认邮箱。
