---
id: flow_chargeback_processing
object_type: Flow
domain: risk-control
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1333395487
tags:
- chargeback
- flow
- end-to-end
subdomain: chargeback
module: null
sensitivity: normal
name: ChargeBack处理端到端流程
aliases: []
related_services: []
related_tables:
- aml.t_risk_case
- aml.t_freeze_order
- aml.t_chargeback_pool
- grc.t_payment_event
related_scenarios:
- scn_chargeback_mail_send_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ChargeBack端到端流程从ChargeBack页面上传收单行（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY）文件开始，系统解析后新增ChargeBack记录，并按记录类型（New case 或 历史记录）触发后续动作：同步CasePool、发送邮件通知、对相关商户进行资金冻结。

## 步骤(跨系统)
1. **上传文件**：在ChargeBack页面上传不同收单行（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY）的文件。
2. **解析并新增ChargeBack记录**：系统解析文件，写入 `aml.t_chargeback_pool`，根据Excel中的 `history flag` 字段判定是否为历史记录（有值则为历史记录）。
3. **判断Case状态**：
   - 若为 **New case (NC)**：执行后续 同步CasePool + 发邮件 + 冻结。
   - 若为 **非New case（仅限历史记录）**：仅同步CasePool，**不发送邮件、不触发冻结**。
4. **同步CasePool**（详见 [[chargeback-casepool-sync]]）：
   - CaseType = `Chargeback`
   - Case Source = `Acquirer`（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY）
   - Memo：VISA/MASTERCARD = `Acquirer + aml.t_chargeback_pool.id + aml.t_chargeback_pool.caseNo`；MAGNATI/ADCB/CKO-HISTORY = `Acquirer + aml.t_chargeback_pool.id`
5. **同步到 `aml.t_risk_case`** 后，触发冻结（仅New case，详见 [[chargeback-freeze-logic]]）：
   - 冻结对象：merchantId（收款方）的DPM账户中的交易金额
   - PSP商户：Memo = `CHB + ARN + auto freeze`，Extension = `caseId + ARN`
   - 非PSP商户：Memo = `CHB + paymentOrderNo + auto freeze`，Extension = `caseId + paymentOrderNo`
   - 写入 `aml.t_freeze_order`
   - 白名单 `chargeback_ignore_frozen_merchant_list` 内的商户ID忽略冻结。
6. **发送邮件通知**（仅New case，详见 [[chargeback-mail-notification]]）：按"邮件总开关 → 是否PSP商户 → ReferredId / 商户邮箱 / 外部商户 / partner_name"的顺序判断收件人组合。

## 涉及服务/表
- 表：
  - `aml.t_chargeback_pool`：ChargeBack记录主表（id、caseNo 等）
  - `aml.t_risk_case`：CasePool同步目标
  - `aml.t_freeze_order`：冻结订单记录（Memo、Extension）
  - `grc.t_payment_event`：用于 VALID=1 判断（有有效记录）
- 配置路径：`Basis → RISK CONTROL → Data Analysis → Risk System Param`
  - `chargeback_ignore_frozen_merchant_list`（冻结白名单）
  - `chargeback_mail_send_outer_switch`、`chargeback_send_mail_product_config`、`chargeback_mail_send_to_default`、`chargeback_mail_send_external_default`、`chargeback_mail_send_psp_default`、`chargeback_mail_receiver_partner_XXXX`（详见 [[chargeback-mail-config]]）

## 校验点
- 记录是否为 **New case**：决定是否触发冻结与发邮件；非New case（历史记录）仅同步CasePool。
- **VALID=1 判断**：在 `grc.t_payment_event` 中存在有效记录。
- **history flag**：Excel中该字段有值则为历史记录。
- **冻结白名单**：商户ID命中 `chargeback_ignore_frozen_merchant_list` 时跳过冻结。
- CasePool 同步字段：CaseType=Chargeback、Case Source=Acquirer、Memo 按收单行规则拼接。
- 冻结记录字段：按PSP/非PSP商户区分 Memo 与 Extension 内容。
- 邮件发送：依据邮件总开关、商户类型（Label=Total Process 判定PSP）、ReferredId、商户邮箱、External、partner_name 综合决定收件人。
