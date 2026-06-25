---
id: flow_jaywan_prepaid_card
object_type: Flow
name: Jaywan 预付卡端到端流程(Dgpay 渠道)
aliases: [Jaywan prepaid card lifecycle, jaywan card lifecycle, dgpay integration]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/877428845 + wiki:b4ddb781 (Jaywan 预付卡设计 / Dgpay 集成 / 用例清单)
tags: [jaywan, prepaid-card, dgpay, mbank, lifecycle, flow]
related_services: [svc_ppc]
related_tables: []
related_scenarios: []
---

# Jaywan 预付卡端到端流程(Dgpay 渠道)

## 概述
Jaywan 品牌预付卡(虚拟卡 + 实体卡)经 Dgpay(供应商,CGS API 提供方)接入的端到端流程:发卡、PIN、激活、交易(provision/balance-inquiry/reversal/declined)、卡状态管理(锁/解锁/关闭/替换)、清算(Clearing)、结算(Settlement)、对账(Reconciliation)。Vendor=Dgpay(我方调用),Institution=mBank/Botim 侧(Dgpay 反向调用)。MBank 为持牌 BIN Sponsor,Botim 管钱包余额与最终授权。环境配置、密钥交换、对账结算、门户报表等机构对接细节见 [[reference_jaywan_mbank_integration]];卡生命周期状态机见 [[scn_card_lifecycle_transitions]]。

## 步骤(跨系统)
1. **公共前置**
   - Key Management:内部 API 取 key + 加解密 API。双方互换 RSA 公钥;请求中我方→Dgpay 敏感字段(如 PIN)用 Dgpay 公钥加密;响应中 Dgpay→我方(卡号、CVV2)用我方公钥加密由我方解密。密钥无指定有效期。
   - Apply vendor token:调 Dgpay `GetToken`;token 持久化、不受重启影响、过期前异步刷新;HTTP Header `Authorization: <token>`,报文 JSON。
   - Generate institution token:实现 Institution `get-token`,供 Dgpay 反向调用,统一做 token 校验。
2. **虚拟卡申请**:前置 Eid KYC、payment password set、identification(密码或生物特征)通过;**同一 EID 同时仅允许一张卡**;Phase 1 不支持无 KYC 的 VIP。调 Dgpay `CreatePrepaidDigitalCard`(CGS:Summary Query / Init Apply / Apply),保存卡号。
   - 错误恢复:`CreatePrepaidDigitalCard` 读超时不可知时,调 `GetPrepaidCards` 拉全部卡比对,识别"超时但已创建"的卡 → 保存入库或 `UpdatePrepaidCardStatus` 关闭。
   - Apply with pay:with pay & with physical card 场景下,收到交易结果后异步申请虚拟卡和实体卡。
3. **PIN 设置**:调 Dgpay `PrepaidCardPinOperation`(Set Card PIN),PIN 用 Dgpay 公钥加密。
4. **查看卡详情**:`GetPrepaidCardInfo` / `GetPrepaidCards`,返回卡号、CVV2 用我方私钥解密。
5. **锁/解锁卡**:`UpdatePrepaidCardStatus`(Lock / Unlock)。
6. **实体卡申请**:`CreatePrepaidEmbossData`(Init Apply / Apply / Tracking),含 pay fee;配送由 Dgpay 负责,Dgpay 反向调 Institution `notify-courier-process` 同步 `CardProcessStatusID`/`CardProcessSubStatusID`(枚举待 Dgpay 提供)。
7. **实体卡激活**:identification 通过且 PIN 已设置后,调 `ActivatePrepaidCard`。
8. **手机号同步**:`UpdateMobilePhoneNumber`,规则:`TelephoneMasterCountryCode`=国码(如 971/86);`TelephoneMasterPhoneCode=left(phone,3)`;`TelephoneMasterPhone`=剩余。
9. **交易处理(Institution API)**:
   - `provision`:集成 risk、payment、bill、pns;处理 Transaction、Refund(dual message)。
   - `balance-inquiry`:返回费后余额(余额不足扣费时返回值待确认 TODO)。
   - `reversal`:含额外 retry;single message reversal 需 reverse settlement 更新。
   - `declined-transaction`:保存被拒交易并按需通知。
   - `update-prepaid-card-status`:Bank Portal 触发,Dgpay 调用 Institution 更新卡状态(institution 响应失败时 Dgpay 侧是否回滚待确认 TODO)。
10. **替换卡(Replace Card)**:Dgpay 无 replace virtual card API;用 `UpdatePrepaidCardStatus` close + `CreatePrepaidDigitalCard` apply 组合(等价 replacement);或等待新 replace API。**不能因此移除换卡功能**。
11. **关闭卡(Close Card)**:`UpdatePrepaidCardStatus`,含 close member check。
12. **清算(Clearing)**:处理 Dgpay Clearing File;明细类型 `DECLINE`(与框架同期)/ `OFFLINE` / `PROVISION` / `BALANCE_INQUERY` / `REVERSAL`(single message reversal 加 reverse settlement update)。
13. **结算(Settlement)**:single message 流程中追加 settlement detail,生成 Settlement File;Settlement 由 Mbank 与 Botim 管理。
14. **对账(Reconciliation)**:与 CS team 对齐对账规则;Reconciliation 由 Botim 负责。
15. **Phase 2 扩展**:Manual Release(人工放行长时间未 post 的 dual message)、`ChargeFee` / `ChargeFeeCancel`(Institution API)、Pending Transaction Chasing(内部机制)。

## 余额持有与同步
- Dgpay 侧不维护余额(pass-through),**无需 balance sync**;`UpdateCardBalance` 为覆盖式更新有并发不一致风险,本期不用。
- 若 Botim 持有余额:请求透传;若 Mbank 持有余额:需余额同步(当前结论为不需要)。

## 关联关系
- **经过的服务(有序)**:Botim/PPC([[svc_ppc]])↔ Dgpay(vendor,外部)↔ Institution(mBank/Botim);集成系统 risk / payment / bill / pns / member / bank portal(待补对象)。(= `related_services` 取已存在的 svc_ppc)
- **关键表**:待补(Jaywan 卡数据落库表未在原文给出物理表名)。
- **关键场景**:卡生命周期状态用例见 [[scn_card_lifecycle_transitions]]。

## Vendor / Institution API 速查
- **Vendor(调用 Dgpay)**:`GetToken`、`CreatePrepaidDigitalCard`(恢复用 `GetPrepaidCards`)、`GetPrepaidCardInfo`、`PrepaidCardPinOperation`、`UpdatePrepaidCardStatus`、`CreatePrepaidEmbossData`、`ActivatePrepaidCard`、`UpdateMobilePhoneNumber`、`NotifyPrintedCards`(bank portal 批量开卡)。
- **Institution(Dgpay 调用我方)**:`get-token`、`provision`、`reversal`、`balance-inquiry`、`declined-transaction`、`update-prepaid-card-status`、`notify-courier-process`、`ChargeFee`/`ChargeFeeCancel`(Phase 2)。
- **对接文档**:Prepaid Card - New Institution Integration Document(DP.00001,dgpays Prepaid,首发 2025-05-21,当前 v1.5);changelog 关键:v1.1 卡号入参由 `ClearCardNumber` 改为 `EncryptedCardNumber`、新增 `GetPrepaidCards`/`ResetPinRetryCount`/`ResetCvv2RetryCount`;v1.2 provision/decline/reversal 新增 `clearingType`;v1.3 新增 `STAN`/`RRN`;v1.4 provision 新增 `IsOfflineTrn`。

## 校验点
- **前置校验**:Eid KYC、payment password、identification 三项均通过;同一 EID 仅一张活跃卡。
- **Token**:vendor token 持久化、不受重启影响、过期前异步刷新;institution token 校验。
- **加解密**:双向公钥;卡号/CVV2 输出端用我方私钥解密;PIN set 用 Dgpay 公钥加密。
- **错误恢复**:CreatePrepaidDigitalCard 超时通过 GetPrepaidCards 对账补偿。
- **Replace 临时方案**:Close + Apply 的资金/状态/通知一致性。
- **清结算**:Clearing 各明细类型字段对齐;Reversal 反向 settlement 更新;单一 settlement 文件中各交易类型分项识别。

## QA 待确认(TODO,原文标注)
- Card Status Update:institution 响应失败时 Dgpay 侧状态是否回滚。
- Balance Inquiry:余额不足扣费场景返回值。
- Courier 状态映射:`CardProcessStatusID` / `CardProcessSubStatusID` 枚举。
- `ProductNumber` / `SubProductNumber` 配置(见 [[reference_jaywan_mbank_integration]] 环境配置,已给出 051/051)。
- Notification 规范(SMS / BOTIM)与 MasterCard Prepaid Card 一致性。
