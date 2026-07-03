---
id: reference_chargeback_business_overview
object_type: Reference
name: ChargeBack业务总览
aliases: [chargeback-business-overview]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: [compliance, wiki-overview]
related_services: [svc_aml]
related_tables: [tbl_aml_t_chargeback_pool, tbl_aml_t_risk_case]
---


# ChargeBack业务总览

ChargeBack页面是风控域下的独立入口，用于上传并解析来自不同收单行的对账文件，添加ChargeBack记录，并联动触发CasePool同步、邮件通知与商户资金冻结。

## 功能定位

- 独立页面入口，直接上传收单行文件
- 解析文件后落库为ChargeBack记录
- 联动后续的同步、通知、冻结等下游动作

完整的端到端处理流程参见 [[flow_chargeback_processing]]。

## 支持的收单行

- VISA
- MASTERCARD
- MAGNATI
- ADCB（目前无记录）
- CKO-HISTORY

## 核心流程

文件上传后系统主要执行以下动作：

1. **添加ChargeBack记录**：解析文件并写入 `aml.t_chargeback_pool`
2. **同步CasePool**：将记录同步到 `aml.t_risk_case`，详见 chargeback-casepool-sync
3. **发送邮件通知**：按多条件路由邮件接收人，详见 chargeback-mail-notification
4. **资金冻结**：对相关商户的DPM账户进行交易金额冻结，详见 chargeback-freeze-logic

## Case 状态对流程的影响

ChargeBack记录的Case状态决定了下游动作是否触发：

- **New case (NC)**：同步CasePool + 发送邮件 + 触发冻结
- **非 New case（仅限历史记录，依据Excel中的 `history flag` 字段判定）**：仅同步CasePool，**不发送邮件**、**不触发冻结**

完整状态枚举与映射见 chargeback-case-status。

## 配置入口

相关开关、白名单、默认收件地址等参数统一配置于：

`Basis → RISK CONTROL → Data Analysis → Risk System Param`（更改后需刷缓存）

具体参数清单参见 chargeback-config-params。

## 关联校验

- **VALID=1 判断**：在 `grc.t_payment_event` 中存在有效记录

## 相关测试场景

邮件发送相关的端到端测试用例集合参见 [[scn_chargeback_mail_send_cases]]。
