---
title: ChargeBack处理流程
domain: risk-control
kind: wiki_page
slug: chargeback-process-flow
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack处理流程

ChargeBack页面通过上传收单行文件，端到端完成记录入库、CasePool 同步、邮件通知与商户资金冻结。

## 入口与支持范围

- 入口：ChargeBack 页面（独立入口），用于上传并解析收单行文件以新增 ChargeBack 记录。
- 支持的 Acquirer：VISA、MASTERCARD、MAGNATI、ADCB（目前无记录）、CKO-HISTORY。
- 业务背景见 [[chargeback-business-overview]]。

## 端到端处理步骤

文件上传后系统按以下顺序处理：

1. 解析文件并新增 ChargeBack 记录入库（`aml.t_chargeback_pool`）。
2. 同步记录到 CasePool（`aml.t_risk_case`）。详见 [[chargeback-casepool-sync]]。
3. 发送邮件通知。详见 [[chargeback-mail-notification]] 与 [[chargeback-mail-config]]。
4. 对相关商户执行资金冻结。详见 [[chargeback-freeze-logic]]。

完整流程图与节点串联参考 [[flow_chargeback_processing]]。

## New Case 与历史记录的处理差异

ChargeBack 记录是否触发后续动作，取决于其 case status，状态枚举与映射见 [[chargeback-case-status]]。

- **New case（NC）记录**：同步到 CasePool + 发送邮件 + 触发冻结。
- **非 New case 记录（仅限历史记录）**：仅同步到 CasePool，**不发送邮件**、**不触发冻结**。
- **历史记录判定**：依据 Excel 中的 `history flag` 字段，有值即视为历史记录。

## VALID 判定说明

- **VALID=1 判断**：`grc.t_payment_event` 中存在有效记录。
- 该判定用于决定 ChargeBack 流程中相关支付事件是否有效，进而影响后续处理。

## 相关测试场景

- 邮件发送相关测试场景集见 [[scn_chargeback_mail_send_cases]]。
