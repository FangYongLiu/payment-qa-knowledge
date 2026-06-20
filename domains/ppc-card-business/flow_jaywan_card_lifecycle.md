---
id: flow_jaywan_card_lifecycle
object_type: Flow
domain: ppc-card-business
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags:
- jaywan
- prepaid-card
- lifecycle
subdomain: null
module: null
sensitivity: normal
name: Jaywan预付卡端到端业务流程
aliases: []
related_services: []
related_tables: []
related_scenarios:
- jaywan-use-case-list
- jaywan-phase1-system-design
- jaywan-clearing-settlement-design
- jaywan-phase2-system-design
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Jaywan预付卡端到端业务流程，覆盖从虚拟卡/实体卡申请、PIN设置、激活、交易(provision/balance-inquiry/reversal/declined)、卡状态管理(锁/解锁/关闭/替换)，到清算(Clearing)与结算(Settlement)、对账(Reconciliation)的完整链路。Vendor 为 Dgpay，Institution 侧为 mBank/Botim 集成。

## 步骤(跨系统)
1. **公共前置**
   - Key Management：内部 api 获取 key，加解密(参考 Encryption Process / gppc-OP-Key Generation)。
   - Apply vendor token：调用 Dgpay `GetToken`，token 持久化、过期前异步刷新；http header 形如 `Authorization: <token>`。
   - Generate institution token：实现 Institution 侧 `get-token`，供 Dgpay 反向调用。

2. **虚拟卡申请 (Create Virtual Card)**
   - 前置条件：Eid KYC、payment password set、identification(payment password 或 biometric) 通过；同一 EID 同时只允许一张卡。
   - 调用 Dgpay `CreatePrepaidDigitalCard`(CGS API: Summary Query, Init Apply, Apply)；保存卡号。
   - 错误恢复：超时或不确定结果时调用 `GetPrepaidCards` 比对，多出的卡可保存或通过 `UpdatePrepaidCardStatus` 关闭。
   - Apply virtual card with pay：with pay & with physical card 场景下，过期已存在未成功 apply，接收交易结果后异步申请虚拟卡和实体卡。

3. **PIN 设置**：调用 Dgpay `PrepaidCardPinOperation`(CGS API: Set Card PIN)；PIN 用我方公钥加密。

4. **查看卡详情**：调用 `GetPrepaidCardInfo` / `GetPrepaidCards`，对返回的卡号、CVV2 用我方私钥解密。

5. **锁/解锁卡**：调用 `UpdatePrepaidCardStatus`(CGS API: Lock / Unlock Card)。

6. **实体卡申请 (Apply Physical Card)**
   - 调用 `CreatePrepaidEmbossData`(CGS API: Init Apply, Apply, Tracking)；流程含 pay fee。
   - 配送由 Dgpay 负责，Dgpay 反向调用 Institution `notify-courier-process` 同步 `CardProcessStatusID` / `CardProcessSubStatusID`。

7. **实体卡激活**：identification 通过且 PIN 已设置后，调用 `ActivatePrepaidCard`。

8. **手机号同步**：会员手机号变更时调用 `UpdateMobilePhoneNumber`，规则：`TelephoneMasterCountryCode` 国码；`TelephoneMasterPhoneCode = left(phone, 3)`；`TelephoneMasterPhone = right part`。

9. **交易处理 (Institution API)**
   - `provision`：集成 risk、payment、bill、pns；处理 Transaction、Refund(dual message)。
   - `balance-inquiry`：返回余额(费后余额)。
   - `reversal`：含额外 retry，single message reversal 需 reverse settlement 更新。
   - `declined-transaction`：保存被拒交易并按需发送通知。
   - Bank Portal 触发：`update-prepaid-card-status` 由 Dgpay 调用 Institution 更新卡状态。

10. **替换卡 (Replace Card)**：Dgpay 当前无 replace virtual card API，使用 `UpdatePrepaidCardStatus` close + `CreatePrepaidDigitalCard` apply 完成替换；或等待新 replace API。

11. **关闭卡 (Close Card)**：`UpdatePrepaidCardStatus`，含 close member check。

12. **清算 (Clearing)**：处理 Dgpay Clearing File；
    - `DECLINE` 在已有流程中加入 settlement detail 生成；
    - `OFFLINE` 清算流程；
    - `PROVISION`、`BALANCE_INQUERY` 清算流程；
    - `REVERSAL` 清算流程，且 single message reversal 增加 reverse settlement update。

13. **结算 (Settlement)**：在 single messages 中追加 settlement detail，生成 Settlement File；Settlement 由 Mbank 与 Botim 管理。

14. **对账 (Reconciliation)**：与 CS team 对齐对账规则，在已有流程中加入 reconciliation flow；Reconciliation 由 Botim 负责，SWITCH 到 host 侧若 Botim 持有余额则也由 Botim 完成。

15. **Phase 2 扩展**：Manual Release(长时间未 post 的 dual message)、`ChargeFee` / `ChargeFeeCancel`(Institution API)、Pending Transaction Chasing(内部机制)。

## 涉及服务/表
- Vendor (Dgpay) API：`GetToken`、`CreatePrepaidDigitalCard`、`GetPrepaidCards` / `GetPrepaidCardInfo`、`PrepaidCardPinOperation`、`UpdatePrepaidCardStatus`、`CreatePrepaidEmbossData`、`ActivatePrepaidCard`、`UpdateMobilePhoneNumber`、`NotifyPrintedCards`、`Courier Notification Service`、`ReplaceCard`(规划中)、`UpdateCardBalance`(若 Mbank 持有余额，本期 pass-through 不需要)。
- Institution API：`get-token`、`provision`、`reversal`、`balance-inquiry`、`declined-transaction`、`update-prepaid-card-status`、`notify-courier-process`、`ChargeFee` / `ChargeFeeCancel`(Phase 2)。
- 文件类：Clearing File、Settlement File。
- 集成系统：risk、payment、bill、pns、member 系统、bank portal。

## 校验点
- **前置校验**：Eid KYC、payment password、identification(密码/生物特征) 三项均通过；同一 EID 仅允许一张活跃卡；Phase 1 不支持无 KYC VIP。
- **Token**：vendor token 持久化、不受重启影响；过期前异步生成新 token；institution token 校验。
- **加解密**：双向公钥；`createCard`/`getPrepaidCardInfo` 输出的卡号、CVV2 用我方私钥解密；PIN set 时用 Dgpay 公钥加密；密钥无指定过期日。
- **错误恢复**：
