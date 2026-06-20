---
title: Jaywan Vendor(Dgpay) Q&A
domain: ppc-card-business
kind: wiki_page
slug: jaywan-vendor-qa
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan Vendor(Dgpay) Q&A

本页汇总与 Dgpay(Vendor) 集成相关的问答，覆盖通用调用、加解密、虚拟/实体卡、卡管理、余额同步、对账结算等。产品侧问题见 [[jaywan-product-qa]]，对接设计见 [[jaywan-phase1-system-design]]、[[jaywan-clearing-settlement-design]]。

## 通用 (Common)

### API 调用样例与定义
- 协议：HTTP，请求/响应均为 JSON。
- 鉴权：将 token 放在 HTTP Header，例如 `Authorization: NWZhMDYwYjAtYjQyZS00OWRhLWE2NmUtNTgxNjM1N2YxMTJi`。

### GetToken
- Dgpay 生成的 token 会持久化，不受系统重启或其他事件影响。
- Institution 侧需实现同样的 token API，供 Dgpay 反向调用。

### 加密与解密
- 双方各自交换公钥：
  - Dgpay 向我方共享其公钥，用于我方在请求中加密敏感数据（如 PIN set 时加密 PIN）。
  - 我方向 Dgpay 共享我方公钥，Dgpay 用其加密响应中的敏感数据（如 `createCard`、`getPrepaidCardInfo` 输出中的卡号、CVV2），由我方解密。
- 加密密钥**无指定过期时间**。
- 详见 [[jaywan-phase1-system-design]] 的 Encryption Process。

### SMS Service
- 当前**未使用**该 API；交易 OTP 不通过此接口下发。

## 虚拟卡 (Virtual Card)

### CreateDigitalCard
- 调用超时恢复方案：通过 `GetPrepaidCards`（即 `GetDebitCardList`）拉取该客户全部卡片，与 Wallet 侧记录比对：
  - 多出的即为超时但已创建成功的卡，可入库或调用 `UpdateDebitCardStatus` 关闭。
- 错误恢复 API 统一为 `GetPrepaidCards`。

### Card Status Update Service
- Institution 响应失败时，Dgpay 侧状态是否回滚：**TODO**。

## 实体卡 (Physical Card)

### NotifyPrintedCards
- 用途：Bank Portal 的批量 onboarding。

### Courier Notification Service
- `CardProcessStatusID`、`CardProcessSubStatusID` 枚举：**TODO**。

### Card PIN
- PIN 不仅用于实体卡，未来 tap pay 等场景也可能使用。

## 卡管理 (Card Management)

### Replace Card
- `ReplaceCard` 方法以 emboss 信息为入参，通常仅用于实体卡。
- 数字卡替换两种方式：
  - 由 Dgpay 扩展支持数字卡 replace；
  - 或先 `UpdateDebitCardStatus` 关闭数字卡，再调用 `createDigitalCard`（流程等价于 replace）。
- 关联用例见 [[jaywan-use-case-list]] 与 [[jaywan-phase2-system-design]] 的 Replace Card / Close Card。

## 余额同步 (Balance Sync)

### UpdateCardBalance
- 该 API 是**全量替换**余额，并发场景下会造成不一致。
- 结论：Dgpay 侧**不维护余额**（pass-through），因此**无需余额同步**。
- 若由 Mbank 持有余额，则需要 balance sync；当前由 Botim 侧持有余额，请求为透传。

## 对账与结算 (Reconciliation & Settlement)

- 结算由 Mbank 与 Botim 共同管理。
- 对账由 Botim 负责；若余额由 Botim 持有，则 SWITCH 到 Host 的对账也由 Botim 完成。
- Settlement 与 Clearing 的报告/格式由 Dgpay 提供给 Botim。
- 详细规则与流程见 [[jaywan-clearing-settlement-design]]。

## 其他 (Other)

- **KYC 信息**：CBUAE 要求银行对 banking-as-a-service 业务保留 KYC 与 KYCC，因此需将客户 KYC 信息传给 Jaywan；具体字段及"仅校验/同时存储"需进一步确认。
- **Chargeback**：由 Botim 收集 chargeback 详情与客户签字，发邮件/表单给 Mbank，由 Mbank 通过 CBUAE 门户发起。
- **运营 Dashboard**：将根据 Botim 需求定制。
