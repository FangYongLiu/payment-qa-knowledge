---
id: domain_jaywan_prepaid_card
object_type: Domain
domain: ppc-card-business
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags:
- jaywan
- prepaid-card
- dgpay
subdomain: null
module: null
sensitivity: normal
name: Jaywan预付卡业务域
aliases: []
related_services: []
related_tables: []
related_scenarios:
- jaywan-prepaid-card-overview
- jaywan-system-design-phases
- jaywan-clearing-settlement-design
- jaywan-dgpay-integration-guide
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Jaywan预付卡业务域指基于Dgpay渠道实现的Jaywan品牌预付卡业务，包含虚拟卡与物理卡的发卡、卡管理、交易处理、清算结算、对账与通知等完整业务能力。该业务域由Botim/Astratech侧（Mbank发卡机构合作）与Dgpay（CGS API供应商）联合实现，覆盖端到端的预付卡生命周期。

## 覆盖范围
- 发卡：Virtual Card 申请（CreatePrepaidDigitalCard）、Physical Card 申请（CreatePrepaidEmbossData）与激活（ActivatePrepaidCard）
- 卡管理：查询卡详情（GetPrepaidCardInfo / GetPrepaidCards）、Lock/Unlock/Replace/Close（UpdatePrepaidCardStatus）、Reset PIN（PrepaidCardPinOperation）、手机号变更同步（UpdateMobilePhoneNumber）
- 交易处理（Institution API）：Provision、Reversal、Balance Inquiry、Declined Transaction
- 物流与状态：Delivery Tracking（NotifyCourierProcess）、Update Card Status from Bank Portal
- 清算结算：Clearing File 处理、Settlement File 生成、Reconciliation
- 基础能力：GetToken（vendor / institution 双向）、Key Management（公钥交换、敏感字段加解密）
- 通知：SMS / BOTIM 通知（参照 MasterCard Prepaid Card 通知规范）
- 范围限制：Phase 1 不支持无 KYC 的 VIP 申请；同一 Eid 同一时间仅允许一张卡

## 关键服务/流程
- 申请前置条件：Eid KYC、payment password set、identification（payment password 或 biometric）通过
- 卡数据：保存卡号；CustomerName/MiddleName/SurName 规则参照 PRD；电话字段拆分为 TelephoneMasterCountryCode、TelephoneMasterPhoneCode（phone number 前 3 位）、TelephoneMasterPhone（剩余部分）
- 加解密：双方互换公钥；卡号、CVV2 在 createCard / getPrepaidCardInfo 输出端解密；PIN 在 PIN set 时加密；密钥无指定过期时间
- Token：Http Header 携带 `Authorization: <token>`；JSON 报文；Token 持久化、不受重启影响；异步在过期前刷新
- 错误恢复：CreateDigitalCard 超时通过 GetPrepaidCards 比对恢复；物理卡申请同样支持自动恢复
- Replace Card：Dgpay 当前无 replace virtual card API，需 Close + Apply 组合实现，或等待新 replace API
- 余额：Dgpay 侧不维护余额，无需 balance sync（pass-through）
- 清结算：Clearing 处理 OFFLINE / PROVISION / BALANCE_INQUERY / REVERSAL / DECLINE 等明细类型；Settlement 在单消息流程中追加 settlement detail 生成；Reconciliation 由 Botim 负责，Settlement 由 Mbank 与 Botim 处理
- Chargeback：Botim 提交表单及客户签字给 Mbank，Mbank 通过 CBUAE 门户发起

## QA 关注点
- 申请并发 / 一 Eid 一卡限制是否被严格执行
- CreatePrepaidDigitalCard 超时后通过 GetPrepaidCards 的对账与补偿正确性
- 加解密：公钥使用范围（请求加密 vs 响应解密）、PIN 加密链路
- Replace Card 临时方案（Close + Apply）的资金、状态、通知一致性
- Card Status Update：institution 响应失败时 dgpay 侧状态是否回滚（待确认 TODO）
- Balance Inquiry 在余额不足扣费场景下的返回值（待确认 TODO）
- Declined Transaction 的存储与通知触达
- Courier 状态映射（CardProcessStatusID / CardProcessSubStatusID 枚举待补充）
- Clearing/Settlement 文件的字段对齐与 Reversal 反向 settlement 更新
- Notification 规范（SMS / BOTIM）与 MasterCard Prepaid Card 一致性
- KYC/KYCC 信息透传给 Mbank 的合规要求（CBUAE）
- ProductNumber / SubProductNumber 配置（gppc-OP-Env Configuration TODO）
