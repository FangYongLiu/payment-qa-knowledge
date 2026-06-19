---
id: flow_chargeback_processing
object_type: Flow
domain: risk-control
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags:
- chargeback
- file-upload
- casepool
- freeze
- mail
subdomain: chargeback
module: null
sensitivity: normal
name: ChargeBack文件上传处理端到端流程
aliases: []
related_services: []
related_tables:
- aml.t_chargeback_pool
- aml.t_risk_case
- aml.t_freeze_order
- grc.t_payment_event
related_scenarios:
- scn_chargeback_mail_send_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ChargeBack页面是独立入口，用于上传并解析来自不同收单行（VISA, MASTERCARD, MAGNATI, ADCB, CKO-HISTORY）的文件，添加ChargeBack记录。文件解析后，系统执行：新增ChargeBack记录 → 同步到CasePool → 发送邮件通知 → 对相关商户进行资金冻结。其中只有 New case 记录会触发邮件发送和冻结，非 New case（历史记录）仅同步到CasePool。

## 步骤(跨系统)
1. **文件上传与解析**：用户在ChargeBack页面上传指定收单行（VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY）的文件，系统解析文件内容。
2. **新增ChargeBack记录**：解析后的记录写入 `aml.t_chargeback_pool`，根据Excel中的 `history flag` 字段判定是否为历史记录（有值则为历史记录）。
3. **判断VALID**：校验 `grc.t_payment_event` 中是否存在有效记录（VALID=1）。
4. **同步到CasePool**：所有记录（含New case和历史记录）同步到 `aml.t_risk_case`，详见 [[chargeback-casepool-sync]]：
   - CaseType = `Chargeback`
   - Case Source = `Acquirer`（具体收单行）
   - Memo 根据收单行不同拼接（VISA/MASTERCARD 含 caseNo；MAGNATI/ADCB/CKO-HISTORY 仅含 id）
5. **判断Case状态**：
   - 若为 **New case (NC)**：继续执行邮件发送和冻结流程。
   - 若为 **非 New case（历史记录）**：流程结束，不发邮件，不冻结。
6. **发送邮件通知**：根据邮件总开关 `chargeback_mail_send_outer_switch`、商户类型（PSP/非PSP）、ReferredId、External、partner_name、商户邮箱等条件，按判断顺序决定收件人。详见 [[chargeback-mail-notification]] 与 [[scn_chargeback_mail_send_cases]]。
7. **资金冻结**：对 New case 记录冻结收款方 merchantId 的 DPM 账户中的交易金额，写入 `aml.t_freeze_order`：
   - PSP商户：Memo=`CHB + ARN + auto freeze`，Extension=`caseId + ARN`
   - 非PSP商户：Memo=`CHB + paymentOrderNo + auto freeze`，Extension=`caseId + paymentOrderNo`
   - 受冻结白名单 `chargeback_ignore_frozen_merchant_list` 控制，名单内商户跳过冻结。详见 [[chargeback-freeze-logic]]。

## 涉及服务/表
- `aml.t_chargeback_pool`：ChargeBack记录主表
- `aml.t_risk_case`：CasePool同步目标表
- `aml.t_freeze_order`：冻结订单表
- `grc.t_payment_event`：用于VALID=1判断的有效支付事件表
- 配置：`Basis → RISK CONTROL → Data Analysis → Risk System Param`（见 [[chargeback-config-params]]）

## 校验点
- **文件来源校验**：仅支持 VISA/MASTERCARD/MAGNATI/ADCB/CKO-HISTORY 五类收单行。
- **VALID=1 判断**：`grc.t_payment_event` 中需有有效记录。
- **历史记录判定**：Excel `history flag` 字段有值即为历史记录，仅同步CasePool，不发邮件、不冻结。
- **New case 触发**：仅 New case (NC) 状态触发冻结与邮件。
- **冻结白名单生效**：`chargeback_ignore_frozen_merchant_list` 配置后需刷缓存才生效。
- **CasePool Memo 拼接规则**：依据Acquirer差异拼接（VISA/MASTERCARD 包含 caseNo，其他不含）。
- **邮件判断顺序**：邮件总开关 → PSP/非PSP → ReferredId/External/partner_name → 商户邮箱（详见 [[chargeback-mail-notification]]）。
- **冻结对象**：始终为 merchantId（收款方）的 DPM 账户中的交易金额。
- **状态枚举映射**：参考 [[chargeback-case-status]] 中 case status → code → desc 的映射表。
