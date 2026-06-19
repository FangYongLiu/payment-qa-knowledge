---
title: ChargeBack业务总览
domain: risk-control
kind: wiki_page
slug: chargeback-business-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack业务总览

ChargeBack页面是风控域内一个独立入口,用于上传并解析多家收单行的对账文件,自动完成 ChargeBack 记录入库、CasePool 同步、邮件通知与商户资金冻结等动作。

## 功能定位

- 独立入口页面,直接上传收单行文件并解析。
- 解析后系统自动执行四类核心动作:
  - 添加 ChargeBack 记录
  - 同步至 CasePool
  - 发送邮件通知
  - 对相关商户进行资金冻结

## 支持的收单行

- VISA
- MASTERCARD
- MAGNATI
- ADCB(目前无记录)
- CKO-HISTORY

## 核心处理动作概览

上传文件后,系统按业务规则触发以下动作,具体规则见对应子页:

- **新增 ChargeBack 记录**:写入 `aml.t_chargeback_pool`。
- **CasePool 同步**:所有记录均会同步,CaseType 为 `Chargeback`,Case Source 为对应 Acquirer。详见 [[chargeback-casepool-sync]]。
- **资金冻结**:仅当记录为 `New case` 时触发,对收款方 merchantId 的 DPM 账户冻结交易金额,并写入 `aml.t_freeze_order`。详见 [[chargeback-freeze-logic]]。
- **邮件通知**:按 PSP/非PSP、是否有 referredId、是否外部商户、是否配置 partner_name 等多条件路由收件人。详见 [[chargeback-mail-notification]] 与 [[chargeback-mail-config]]。

## Case 状态对处理动作的影响

Case 状态决定了哪些动作会被触发:

- **New case (NC)**:同步 CasePool + 发送邮件 + 触发冻结。
- **非 New case(仅限历史记录,Excel 中 `history flag` 有值)**:仅同步 CasePool,**不发送邮件**,**不触发冻结**。

完整状态枚举与映射见 [[chargeback-case-status]]。

## 端到端处理流程

完整处理时序(含 `VALID=1` 在 `grc.t_payment_event` 是否存在有效记录的判断)见 [[chargeback-process-flow]] 与 [[flow_chargeback_processing]]。

## 相关页面

- [[chargeback-freeze-logic]] — 冻结对象、Memo/Extension 规则与白名单配置
- [[chargeback-casepool-sync]] — CasePool 同步字段细节
- [[chargeback-mail-notification]] — 邮件路由判断顺序
- [[chargeback-mail-config]] — 邮件相关 Risk System Param 配置项
- [[chargeback-case-status]] — Case 状态枚举与 code 映射
- [[chargeback-process-flow]] — 处理流程图与关键节点
- [[scn_chargeback_mail_send_cases]] — 邮件发送 TS001~TS012 测试场景集
