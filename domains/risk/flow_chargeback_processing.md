---
id: flow_chargeback_processing
object_type: Flow
name: ChargeBack文件上传处理端到端流程
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
- file-upload
- casepool
- freeze
- mail
related_scenarios:
- scn_chargeback_mail_send_cases
---

# ChargeBack文件上传处理端到端流程

## 概述
ChargeBack 页面是风控域下的独立入口,上传并解析来自不同收单行(VISA / MASTERCARD / MAGNATI / ADCB / CKO-HISTORY)的对账文件,新增 ChargeBack 记录。文件解析后系统执行:新增 ChargeBack 记录 → 同步到 CasePool → 发送邮件通知 → 对相关商户资金冻结。**仅 New case (NC) 记录触发邮件发送和冻结**;非 New case(历史记录)仅同步到 CasePool。

> 涉及的后台服务在当前域内未识别到对应 service 对象(待补);相关 `aml.*` 表暂未建独立 Table 对象,本流程用纯文字引用(待补)。

## 步骤(跨系统)
1. **文件上传与解析**:用户在 ChargeBack 页面上传指定收单行文件,系统解析。
2. **新增 ChargeBack 记录**:解析后写入 `aml.t_chargeback_pool`(待补:未建 Table 对象),依据 Excel `history flag` 字段判定是否为历史记录(有值即历史记录)。
3. **判断 VALID**:校验 `grc.t_payment_event`([[tbl_grc_t_payment_event]])中是否存在有效记录(VALID=1)。
4. **同步到 CasePool**:所有记录(含 New case 与历史记录)同步到 `aml.t_risk_case`(待补):
   - `CaseType` = `Chargeback`
   - `Case Source` = `Acquirer`(具体收单行:VISA / MASTERCARD / MAGNATI / ADCB / CKO-HISTORY)
   - `Memo`:VISA / MASTERCARD = `Acquirer + id + caseNo`;MAGNATI / ADCB / CKO-HISTORY = `Acquirer + id`
5. **判断 Case 状态**:New case (NC) → 继续邮件 + 冻结;非 New case(历史记录)→ 流程结束,不发邮件不冻结。
6. **发送邮件通知**:按"邮件总开关 → PSP/非PSP → ReferredId → 外部商户/partner_name → 商户邮箱"多级判断决定收件人,详见 [[scn_chargeback_mail_send_cases]]。
7. **资金冻结**:对 New case 记录冻结收款方 merchantId 的 DPM 账户交易金额,写入 `aml.t_freeze_order`(待补):
   - PSP 商户(`Label = Total Process`):Memo=`CHB + ARN + auto freeze`,Extension=`caseId + ARN`
   - 非 PSP 商户:Memo=`CHB + paymentOrderNo + auto freeze`,Extension=`caseId + paymentOrderNo`
   - 受冻结白名单 `chargeback_ignore_frozen_merchant_list` 控制,名单内商户跳过冻结。

## ChargeBack Case 状态枚举
| case status | code | desc |
|---|---|---|
| WON | WON | WON |
| ARBITRATION_LOST | ALOST | ARBITRATION LOST |
| ARBITRATION_RAISED | AR | ARBITRATION RAISED |
| LOST | LOST | LOST |
| IN_CYCLE | IC | IN CYCLE |
| FULFILLED | IC | FULFILLED |
| CHBK_ACCEPTED_BY_MERCHANT | LOST | CHBK ACCEPTED BY MERCHANT |
| NO_RESPONSE_BY_MERCHANT | LOST | NO RESPONSE BY MERCHANT |
| NEW_CASES | NC | NEW CASES |

注:`FULFILLED` 与 `IN_CYCLE` 共用 code `IC`;`CHBK_ACCEPTED_BY_MERCHANT` / `NO_RESPONSE_BY_MERCHANT` 与 `LOST` 共用 code `LOST`。

## 关键配置(Risk System Param)
路径:`Basis → RISK CONTROL → Data Analysis → Risk System Param`(配置存 [[tbl_aml_t_system_param]],改后须刷缓存)。
| 配置项 | 含义 |
|---|---|
| `chargeback_mail_send_outer_switch` | 邮件总开关(yes/no) |
| `chargeback_send_mail_product_config` | 业务产品码白名单 |
| `chargeback_mail_send_to_default` | 默认邮件地址(亦作"邮件开关"判定字段) |
| `chargeback_mail_send_external_default` | 外部邮件地址 |
| `chargeback_mail_send_psp_default` | PSP 默认邮件地址(PSP 默认 6 邮箱) |
| `chargeback_mail_receiver_partner_XXXX` | 按 partner_name 配置收件邮箱(主要用于 remittance 渠道) |
| `chargeback_ignore_frozen_merchant_list` | 冻结白名单,名单内 merchantId 跳过冻结 |

## 关联关系
- **关键表**:`grc.t_payment_event`([[tbl_grc_t_payment_event]]);`aml.t_chargeback_pool` / `aml.t_risk_case` / `aml.t_freeze_order`(待补:未建对象);配置表 [[tbl_aml_t_system_param]]。
- **关键场景**:[[scn_chargeback_mail_send_cases]](= `related_scenarios`)。

## 校验点
- **文件来源校验**:仅支持 VISA / MASTERCARD / MAGNATI / ADCB / CKO-HISTORY 五类收单行。
- **VALID=1 判断**:`grc.t_payment_event` 中需有有效记录。
- **历史记录判定**:Excel `history flag` 有值即历史记录,仅同步 CasePool,不发邮件不冻结。
- **New case 触发**:仅 New case (NC) 触发冻结与邮件。
- **冻结白名单生效**:`chargeback_ignore_frozen_merchant_list` 配置后需刷缓存。
- **CasePool Memo 拼接规则**:VISA/MASTERCARD 含 caseNo,其他不含。
- **冻结对象**:始终为 merchantId(收款方)DPM 账户中的交易金额。
